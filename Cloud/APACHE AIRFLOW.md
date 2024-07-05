**workflow**: Workflow can be your simple calculation, creating infrastructure, perform some query in the database, bash command, python script, MySQL queries, Hive queries, etc. Workflow is divided into one or more than one task which relates to each other and forms a  DAG (Directed Acyclic Graph).

**DAG**: DAG is a collection of all small task which joins together to perform a big task.

**Apache Airflow: *Airflow is a platform to programmatically author, schedule, and monitor workflows.***

**Basic Concepts:**

* Tasks: It is the  basic unit of execution .
  * **Operators**: They are pre-defined templates used to build most of the Tasks.
  * **Sensors**: They are a unique subclass of Operators and have only one job — to wait for an external event to take place so they can allow their downstream tasks to run.
  * **TaskFlow**: It was recently added to Airflow, and provides the functionality of sharing data in a data pipeline.
* Directed Acyclic Graphs: **DAG is a graph** with nodes connected via directed edges and has **no cyclic edges** between the nodes. In Airflow, the Tasks are the nodes, and the directed edges represent the dependencies between Tasks.
* Control Flow: A DAG has  directed edges connecting nodes  (tasks) that interjoins two or more  **tasks** . It defines the carryout workflow within a DAG.
* Task instance: **Execution** of a single  **task** . They also indicate the **state of the Task,** such as “running”, “success”, “failed”, “skipped”, “up for retry”, etc.
* DAGrun: When a DAG is triggered in Airflow, a DAGrun object is created. DAGrun is the instance of an executing DAG. It contains a timestamp at which the DAG was instantiated and the  state (running, success, failed) of the DAG. DAGruns can be created by an **external trigger** or at **scheduled intervals** by the scheduler.
* **Sensors** : Sensors are a specialized type of operator that waits for a certain criterion to be met before proceeding with the execution of downstream tasks. For example, a file sensor can wait for the existence of a file before triggering the next task.
* **Hooks** : Hooks are a way to interact with external systems or databases. They provide a consistent interface for connecting to various services and are used by operators to perform specific actions.
* **XComs:** XComs facilitate communication and data exchange between tasks within a DAG. They allow tasks to share data, such as variables or results, by pushing and pulling values between tasks.
* **Connections:** Connections in Airflow represent the configuration details required to connect to external systems or services. They store information such as database
  credentials, API keys, and connection URLs.
* **Taskflow:** Taskflow API is a higher-level abstraction in Airflow that offers advanced features and flexibility for defining complex workflows and dependencies. It provides a more intuitive way to structure and manage workflows, utilizing the power of DAGs and operators.

**Components of Apache Airflow:**

1. **DAG (Directed Acyclic Graph)**: A DAG is a collection of tasks with defined execution dependencies. Each node in the graph represents a
   task, and the edges define the order of execution. DAGs make it easy to visualize and manage complex workflows.
2. **Scheduler**: The scheduler is responsible for determining when to execute each task in a DAG based on the defined dependencies and schedules. It ensures that tasks are executed in the correct order and at the right times.A scheduler has two tasks: To trigger the scheduled DAGs.To submit the tasks to the executor to run.
3. **Workers**: Workers are the actual execution environments where your tasks run. They pull tasks from the scheduler and execute them. Airflow supports various worker types, including celery, Kubernetes, and more.
4. **Metadatabase:** Airflow uses a metadata database to store credentials, connection information, history, and configuration. This database is crucial for tracking the status and history of your workflows.
5. **Web Interface**: Airflow provides a web-based UI for monitoring and managing your DAGs, including viewing task logs, retrying failed tasks, and triggering DAG runs.
6. **Executor** : It is the **mechanism **that handles the running of tasks. Airflow has many executors, primarily Sequential Executor, Local Executor, and Debug Executor. There also exist remote executors for complex problems, such as Celery Executor, Dask Executor, Kubernetes Executor, and CeleryKubernetes Executor.

**Working of the Airflow Components:**

* The Scheduler constantly continues tapping the dag directory and makes an entry for **each DAG** in the database.
* The airflow parser parses the DAGsand creates the DAGRuns. The Scheduler also creates instances of the tasks that require execution.
* All these tasks are marked “ **scheduled** ” in the database.
* The primary scheduler then takes these tasks and sends them to a  **queue** . These tasks are then marked as “ **queued** ”.
* The executor fetches the task from the scheduler queue and assigns them to the workers.

---

**How to handle tasks that get stuck in a queued state?**

This can be intentional due to various reasons like airflow parallelism have been reached or slots are full. It can also be unintentional when something fails between the executor and scheduler. We can track such tasks by querying the airflow db.

```sql
SELECT dag_id, run_id, task_id, queued_dttm
FROM task_instance
WHERE queued_dttm < current_timestamp - interval '30 minutes' AND state = 'queued'
```

**Explain XCom and its limitations.**

XComs, short for Cross-Communication, is a mechanism for tasks to exchange small pieces of data. It is used to share metadata and configuration parameters. It can also pass small pieces of data between tasks.

```sql
# In source task: task id -> ti_1
kwargs['ti_1'].xcom_push(key='data_key', value='data_value')

# In sink / consumer task:
extracted_data = ti.xcom_pull(task_ids='ti_1', key='data_key')
```

**Limitations:**

* XComs are stored in the Airflow database. So we should only pass a small amount of info in XCom or else it will overload the database.
* XComs are stored in an airflow db without encryption. So it will be a risk to share sensitive info using XCom.
* XComs are serialized for exchange. By default, Airflow uses JSON serialization or pyarrow serialization. So we are limited to objects that can be serialized.
* Designed for Write Once, Read many times. But if we use a mutable data structure for the data container multiple tasks can mutate the Xcom.
* On every retry, XComs will be cleared and new XComs will be created for the task instance.
* When exchanging data between two dags— both DAGs must have the same execution date.

**Explain Sensor in Airflow. In which scenario we should use poke vs reschedule mode?**

A sensor is a type of operator that for a condition at a specific interval (`poke_interval`). If the condition is met the task is marked successful. Otherwise, the sensor waits for another interval before checking again. For a Sensor, there are two modes. 1. Poke 2. Reshedule.

In `poke` mode, the sensor occupies a worker slot for the entire execution time and sleeps between pokes. While in `reschedule` mode if the condition is not fulfilled then the sensor releases its worker slot and reschedules the next check for a later time.

So if our `poke_interval` is very short (less than about 5 minutes), we should use the `poke` mode. Using `reschedule` mode in this case can overload our scheduler. For long-running sensors, we should opt for `reschedule`.

**How is parallelism controlled or managed in Airflow?**

Parallelism in Airflow is controlled at multiple levels. At the system/installation level, there is core parallelism. This decides how many tasks can run at the same time for that scheduler. Then we have parallelism at the DAG run level which controls how many instances of the same dag can be run at the same time. We can also how many tasks can run for a particular dag in parallel. The following configurations control the various aspects of parallelism in Airflow.

```python
core.parallelism * number of schedulers
core.max_active_tasks_per_dag
core.max_active_runs_per_dag
core.default_pool_task_slot_count
max_active_tis_per_dag
```

**How do we define dependencies between tasks?**

Dependencies decide the flow of operation for a DAG. It controls the order in which task(s) are executed. There are four major ways to define task dependencies in Airflow:

```
set_upstream() [<<]
set_downstream()[>>]
chain()
chain_linear()
cross_downstream() only since 2.7+
inferred dependencies via the TaskFlow API
depends_on_past #task depends on the success of the previous run of the same task
```

```
t0.set_downstream(t1) | t1.set_upstream(t0)
t0 >> t1 | t1 << t0

chain(*list_of_tasks)
chain_linear(*list_of_tasks)

demo_function_1(demo_function_2()) # Inferred
```

**What are hooks and why do need them?**

Hooks are abstractions to APIs of external systems like Hive, S3, MySQL, Postgres, HDFS, and Pig. Hooks implement a common interface when possible, and act as a building block for operators. They use connections to configure the auth of the external system. Operators call/use Hooks when they need to interact with external systems. Hooks allow code reusability and modularity. We can remove a lot of boilerplate code if we leverage Hooks.

**What are the different states a Task can be in? What are the happy path transitions of a Task?**

* **None:** The task is defined.
* **scheduled:** The task dependencies are met, and has been assigned a scheduled interval, and are ready for a run.
* **Queued:** The task is assigned to an executor, waiting to be picked up by a worker.
* **Running:** The task is running on a worker.
* **Success:** The task has finished running, and got no errors.
* **Shutdown:** The task got interrupted externally to shut down while it was running.
* **Restarting:** The task got interrupted externally to restart while it was running.
* **Failed:** The task encountered an error.
* **Skipped:** The task got skipped during a dag run due to branching
* **upstream_failed:** An upstream task, the task on which this task had dependencies, failed.
* **up_for_retry:** The task had failed but is ongoing retry attempts.
* **up_for_reschedule:** The task is waiting for its dependencies to be met (It is called the “Sensor” mode).
* **deferred:** The task has been postponed.
* **Removed:** the task has been taken out from the DAG while it was running.

Happy path of states for a task will be:  **none → scheduled →queued → running → success** .

**What are trigger_rules in Airflow?**

Trigger Rules define the conditions under which a task should be executed based on its upstream tasks’states.

* **all_success:** the task gets triggered when all upstream tasks have succeeded.
* **all_failed:** the task gets triggered if all of its parent tasks have failed.
* **all_done:** the task gets triggered once all upstream tasks are done with their execution irrespective of their state, success, or failure.
* **one_failed:** the task gets triggered if any one of the upstream tasks gets failed.
* **one_success:** the task gets triggered if any one of the upstream tasks succeeds.
* **none_failed:** the task gets triggered if all upstream tasks have finished successfully or been skipped.
* **none_skipped:** the task gets triggered if no upstream tasks are skipped, irrespective of whether they succeeded or failed.

**What are macros in Airflow?**

Macros, on the other hand, are predefined functions provided by Airflow that can be called directly within Jinja templates. They offer additional functionality such as execution date manipulation, branching, and more. Some common macros include `<span> </span>{{ ds }}, {{ ts }}, {{ execution_date }}` .

**Explain the catch_up parameter in the Airflow DAG definition.** 

The `catch_up` parameter in Airflow is a configuration setting that determines how the scheduler should handle the execution of tasks for a DAG (Directed Acyclic Graph) when it starts running.

How do you define cross-dag dependency?

Cross-DAG dependencies allow us to establish relationships between tasks in different DAGs. There are four ways to do this.

> Sensor
> Trigger
> Dataset (Only for airflow version 2.4+)
> API

**What are callback functions?**

The callback provides a way to act upon changes in the state of a given task or DAG. There are 5 major callbacks.

on_success_callback → Invoked when the task succeeds
on_failure_callback → Invoked when the task fails
sla_miss_callback → Invoked when a task misses its defined SLA
on_retry_callback → Invoked when the task is up_for_retry
on_execute_callback → Invoked right before the task begins executing

**Can you explain the Cluster Policy in Airflow? Give some examples where they can be used.**

Cluster policies allow us to check or mutate DAGs or Tasks on an Airflow cluster. There are three main types of cluster policy:

* **dag_policy** : This policy gets executed at load time of the DAG.
* **task_policy** : This policy gets executed when the task is created during parsing of the task from DagBag at load time.
* **task_instance_mutation_hook** : This policy to the instance of a task just before the task instance is executed.
* **pod_mutation_hook:** allows us to modify the configuration of Kubernetes pods at runtime, just before the pod is launched. This function is defined in the `airflow_local_settings.py` file.
* **get_airflow_context_vars**

**Order in which these are invoked:**

Dag Policy → Task Policy → task_instance_mutation_hook → pod_mutation_hook

**What are Pools in airflow and why do we use it? Pools are useful for managing shared resources.**

In Airflow, `pools` is a concept that enables resource management and concurrency control within our workflows. It also helps in prioritizing tasks. Pools allow us to limit the number of task instances that can run simultaneously for a specific set of tasks. Tasks can then be assigned to a pool by using the `pool` parameter when creating tasks. Each pool has a defined size or limit, and when the limit is reached, new task instances will be queued and wait for a slot to become available. If tasks are not given a pool, they are assigned to `default_pool` which is initialized with 128 slots.

**Explain the difference between KubernetesExecutor and KubernetesPodOperator.**

In airflow, an operator deals with what to do (in a task) and an executor deals with how to do the task. KubernetesExecutor — Submits **task** on K8s
and KuberentesPodOperator — Submits **task code** on K8s.

**How can we run the same dag again once the current run is over? This process should keep on repeating.**

We can achieve this in two ways. The first approach is to add a Task at the end of the DAG. In this task, we use TriggerDagRunOperator to trigger itself again.

```
task1 >> task2 >> task3 >> task4 [TriggerDagRunOperator(trigger_dag_id='current_dag_id')]

```

Second Approach: Since Airflow 2.6 we can use the `@continuous` schedule. This will keep the DAG running always.

**What is a ShortCircuitOperator?**

ShortCircuitoperator allows a pipeline to continue based on the result of the python_callable supplied to the task. If the returned result is False the pipeline will be short-circuited. Downstream tasks will be marked with a state of **skipped** if `ignore_downstream_trigger_rules` is set to True. When we set `ignore_downstream_trigger_rules`to `False`, the direct downstream tasks are still skipped, but the trigger rules for other **subsequent **downstream tasks are respected.

If the returned result is True, downstream tasks proceed as normal, and one `XCom` of the returned results is pushed.

**Explain RBAC in Airflow.**

Airflow RBAC is a model built into Airflow that allows for managing users, their permission, and their role in Airflow UI/API. It is built on Flask App Builder.

**What are ExternalPythonOperator & BranchExternalPythonOperator?**

These operators allow us to run our Python code in a virtual environment, isolated from the worker. This helps us in scenarios where worker env has conflicts with the runtime code dependencies.

**How can you trigger a specific task in an Airflow DAG manually?**

We can do this either via UI or CLI. The CLI command to do so is the following:

```
airflow run <DAG_ID> <TASK_ID> <EXECUTION_DATE>
# DAG_ID -> ID of the DAG
# TASK_ID -> ID of the Task
# EXECUTION_DATE -> execution date in YYYY-MM-DD format
```

**How do you only run the specific task(s) of a DAG for a backfill?**

We can leverage the `--task_regex` parameter to selectively backfill only specific tasks.

```
airflow backfill -s <start_date> -e <end_date> -t <tast_regex> <dag_id>
# airflow backfill -s 2022-01-01 -e 2022-01-31 -t [load|transform]_* card_processing_dag
```

**What is the significance of the ‘provide_context’ parameter in the Airflow Operator?**

The `provide_context` parameter is a boolean parameter that controls whether the operator should be passed the entire context dictionary during execution. This set of kwargs correspond exactly to the [context variables](https://airflow.apache.org/docs/apache-airflow/stable/templates-ref.html#templates-variables) you can use in your Jinja templates. The context dictionary holds information about the execution date, task ID, DAG ID, DAG run ID, and other metadata.

**What are SLAs in Airflow?**

Service Level Agreement refers to an agreement between stakeholders that specifies the maximum allowable duration for a DAG or Task to complete.

**How does Airflow handles task retries?**

irflow offers three parameters `retries`, `retry_delay` and `retry_exponential_backoff` to decide in how and when to retry a failed task. When Exponential backoff is enabled it double the wait time between retries after every retry.

**Explain, how airflow security works.**

Airflow has built the role-based access control (RBAC) of the web console on top of Flask AppBuilder (FAB). A user can have multiple roles and different users can share the same role. Each role can have multiple permissions. Each permission allows the user an action against a resource.

Airflow provides 5 default roles with predefined permissions:

> Admin, Public, User, Public, Viewer ad Op.

In addition, Airflow provides an interface that allow users to define their own `SECURITY_MANAGER_CLASS`. We can define our own auth logic in your security manager.

Since Airflow UI is based on FAB, it also supports 5 auth types:

> Database | OAuth | OpenID | LDAP | REMOTE_USER

**How do you handle sensitive variables in Airflow.**

By default, airflow considers your variable secret if your variable name has a string like the following:

> access_token | api_key | apikey | authorization | passphrase | passwd | password | private_key | secret | token

We can also add our own custom names that will be considered sensitive by Airflow by setting the following env variable.

> AIRFLOW__CORE__SENSITIVE_VAR_CONN_NAMES — A comma-separated list of extra sensitive keywords to look for in variables names or connection’s extra JSON.


**Explain Airflow metadata. How can we access this?**

In Airflow, metadata refers to the information and configuration details about workflows, tasks, connections, and other components within the Airflow system. This metadata is typically stored in a metadata database, which is usually backed by a SQL-based database such as SQLite, MySQL, or PostgreSQL. Airflow uses this metadata to manage and orchestrate workflows, track task statuses, handle retries, and provide visibility into workflow execution.

We can access this data by connecting it to the backend DB.

In many managed solutions (MWAA) we might not have direct access to the database. We can still access this metadata using `airflow.models`.

**Have you encountered an error with the message “Return code -9”? What does it mean & how to handle this?**

Return code -9 is mostly associated with an out-of-memory error. The task instance is taking more memory than configured. We can configure the worker’s memory setting to fix the issue.

This error might also arise due to large XCOM objects. We should use remote storage (object store or shared file system) for intermediate data and pass its reference to the consumer task.



## What is a zombie task in Airflow?

A zombie task is one that the Airflow database thinks is running but hasn’t emitted a heartbeat for a certain amount of time.

Or Zombie tasks are tasks in Airflow that have completed execution, but are still present in the task list and marked as “running.” This can occur when a task finishes execution but the Airflow worker process dies before it can mark the task as “success” or “failed.” As a result, the task remains in the “running” state and becomes a zombie.

There are a lot of things that can cause zombies. Some examples include:

* worker process dies (runs out of memory) before it can mark the task as “success” or “failed”.
* The network connection between the worker and Airflow database is severed.
* long-running tasks not sending any signal/log to ensure its liveness

To avoid this:

* increase the scheduler configuration *scheduler_zombie_task_threshold* from default 5 minutes to somewhere around ~20–30 minutes.
* set `AIRFLOW__SCHEDULER__SCHEDULER_ZOMBIE_TASK_THRESHOLD` to a value higher than the DAG file parsing interval
* Keep emitting logs from Kubernetes pods at an interval less than *scheduler_zombie_task_threshold, *logging actions will confirm that the pod is still alive.



**How do you get access to the current context in task instances?**

By using the following code we can access the context:

```
from airflow.operators.python import get_current_context
context = get_current_context()

foo = context["dag_run"].conf["foo"]
```


**Explain the purpose of the `start_date` and `end_date` parameters in an Airflow DAG.**

In Apache Airflow, the `start_date` and `end_date` parameters in a Directed Acyclic Graph (DAG) play a crucial role in determining when the DAG is eligible to run.

The `start_date` is not just the initial run date; it also defines the anchor point for the DAG's schedule. The scheduler won't consider running the DAG before this date.

The `end_date` parameter specifies the latest point in time until which the scheduler should consider running the DAG. It defines the time window during which the scheduler should create new runs.


## What are some of the most useful Airflow CLI commands?

* List DAGs: airflow list_dags
* Show DAG details: airflow show_dag <DAG_ID>
* List tasks for a DAG: airflow list_tasks <DAG_ID>
* Show task details: airflow task_info <DAG_ID> <TASK_ID> <EXECUTION_DATE>
* Trigger a DAG run: airflow trigger_dag <DAG_ID>

## What is Data Lineage?

Data lineage describes the end-to-end journey of data, starting from its origin (source) to its final destination (target), including all the intermediate steps and transformations it undergoes.


## Write a Python code to download a file from GCS to local system using airflow.


```python
from datetime import datetime, timedelta
from airflow import DAG
from airflow.providers.google.transfers.gcs_to_local 
import GoogleCloudStorageToLocaFileSystemOperator


# Define default_args for the DAG
default_args = {
    'owner': 'airflow',
    'start_date': datetime(2023, 1, 1),
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}


# Instantiate the DAG
dag = DAG(
    'gcs_to_local_example',
    default_args=default_args,
    description='Example DAG to download a file from GCS to local system',
    schedule_interval=timedelta(days=1),
)


# Define the task to download a file from GCS to local system
gcs_to_local_task = GoogleCloudStorageToLocaFileSystemOperator(
    task_id='download_from_gcs',
    bucket_name='your_gcs_bucket_name',
    object_name='path/to/your/file/in/gcs.txt',
    destination_path='/path/on/local/system/downloaded.txt',  # Change this to your desired local path
    gcp_conn_id='google_cloud_storage_default',  # Connection ID for GCS, configure in Airflow UI
    task_concurrency=1,  # Set concurrency to 1 to avoid issues with concurrent downloads
    dag=dag,
)

# Set the task in the DAG
dag

# Set the task in the DAG
dag
```

**workflow**: Workflow can be your simple calculation, creating infrastructure, perform some query in the database, bash command, python script, MySQL queries, Hive queries, etc. Workflow is divided into one or more than one task which relates to each other and forms a  **DAG ** (Directed Acyclic Graph).

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
* The executor **fetches the task from the scheduler queue and assigns them to the workers.

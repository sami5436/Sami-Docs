# Apache Airflow Overview

## Introduction
Apache Airflow is an open-source platform to programmatically author, schedule, and monitor workflows. It allows you to define workflows as Directed Acyclic Graphs (DAGs) of tasks, enabling complex data pipelines and automation

## Core Concepts

### Directed Acyclic Graphs (DAGs)
A DAG is a collection of tasks organized in a way that reflects their relationships and dependencies. In Airflow, a DAG defines the structure of your workflow, specifying the order in which tasks should be executed. Each DAG runs on a schedule and can be triggered manually 
### Tasks
Tasks are the basic unit of work in Airflow. They represent individual steps in a workflow, such as running a script, querying a database, or sending an email. Tasks are defined using operators, which are predefined templates for common operations 

### Operators
Operators are the building blocks of tasks in Airflow. They define what action to perform. Common operators include:
- **BashOperator**: Executes a bash command.
- **PythonOperator**: Executes a Python function.
- **EmailOperator**: Sends an email.
- **HttpOperator**: Makes an HTTP request

### Scheduler
The scheduler is responsible for triggering scheduled DAGs and tasks. It monitors the DAGs and ensures that tasks are executed at the right time and in the correct order

### Executor
The executor determines how tasks are executed. Airflow supports different executors, such as the **LocalExecutor** (for running tasks locally) and the **CeleryExecutor** (for distributed task execution)

### Web Interface
Airflow provides a web-based user interface to monitor and manage workflows. The UI allows you to visualize DAGs, track the progress of tasks, and view logs
## How Airflow Works

1. **Define DAGs**: You define your workflows as DAGs using Python code. Each DAG file contains the DAG definition and the tasks it includes.
2. **Schedule DAGs**: The scheduler triggers DAGs based on their schedule interval or external triggers.
3. **Execute Tasks**: The executor runs the tasks defined in the DAGs, ensuring they are executed in the correct order and handling retries in case of failures.
4. **Monitor Workflows**: The web interface allows you to monitor the status of your workflows, view logs, and troubleshoot issues

## Example DAG File

Here's a simple example of a DAG file:

```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime, timedelta

# Default arguments for the DAG
default_args = {
    'depends_on_past': False,
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}

# Define the DAG
dag = DAG(
    'example_dag',
    default_args=default_args,
    description='A simple tutorial DAG',
    schedule_interval=timedelta(days=1),
    start_date=datetime(2023, 1, 1),
    catchup=False,
    tags=['example'],
)

# Define tasks
t1 = BashOperator(
    task_id='print_date',
    bash_command='date',
    dag=dag,
)

t2 = BashOperator(
    task_id='sleep',
    bash_command='sleep 5',
    retries=3,
    dag=dag,
)

t3 = BashOperator(
    task_id='templated',
    bash_command='echo "{{ ds }}"',
    dag=dag,
)

# Set task dependencies
t1 >> [t2, t3]
```

### Explanation
- **default_args**: Default arguments for all tasks in the DAG.
- **dag**: The DAG object, defining the workflow.
- **tasks**: Individual tasks using BashOperator.
- **dependencies**: Task dependencies, specifying the order of execution



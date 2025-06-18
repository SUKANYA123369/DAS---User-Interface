## DAS (Data Analytics System) – User Interface

This project is a Streamlit-based web interface that allows users to process and execute Python scripts stored in HDFS, track and manage their status via MongoDB, and monitor detailed logs through a logging mechanism. It integrates Apache Spark for distributed computation of the uploaded scripts.

### Technologies Used

1. Python  
2. Streamlit  
3. Apache Spark  
4. HDFS  
5. MongoDB  
6. Logging  
7. Subprocess  
8. Pandas  

### Workflow Overview

1. Connect to HDFS and MongoDB using InsecureClient and MongoClient  
2. List files in the HDFS directory  
3. New files are inserted into MongoDB with status: `pending`  
4. Streamlit UI displays available `.py` files for execution  
5. User can preview code, select files, and set retry count  
6. Selected `.py` files are executed using `spark-submit`  
7. Execution results are logged and MongoDB is updated  
8. Retries are attempted if execution fails  
9. Logging is written to `logfile.log`  
10. MongoDB tracks file execution status: `pending`, `success`, `failed`  

### Configuration

The configuration file is located at: [`config.py`](config.py)

This file contains the following settings:

- **HDFS URL**: `http://localhost:50070`  
- **HDFS Directory**: `/my_project/scripts`  
- **MongoDB URI**: Connects to MongoDB Atlas cluster  
- **MongoDB Database**: `project`  
- **MongoDB Collection**: `sample`

> 📌 This configuration sets up connections for HDFS and MongoDB, enabling data storage and retrieval for the application.

### Logging

The logging configuration is defined in: [`logger_setup.py`](logger_setup.py)

This module sets up a flexible logging system that:

- Accepts `--debug` to enable debug-level logs  
- Accepts `--log-file` to specify the log file path (default: `logfile.log`)  
- Logs messages to both console and file  
- Formats logs as: `timestamp - log level - message`  

### Execution Manager

Main execution logic is implemented in: [`execution_manager.py`](execution_manager.py)

This class automates the execution of Python scripts stored in HDFS and tracks their statuses in MongoDB. It includes:

- **HDFS Integration**: Reads available Python files from HDFS  
- **MongoDB Integration**: Logs and tracks execution status (`pending`, `success`, `failed`)  
- **Streamlit Interface**:
  - View `.py` file previews  
  - Select files to execute  
  - Set retry counts  
- **Spark Submit**: Executes scripts via `spark-submit`  
- **Error Handling & Retry**: Automatically retries failed scripts  

> 📌 Supports execution tracking, preview, and retries with a rich UI using Streamlit.

### Streamlit UI

The main entry point for the Streamlit dashboard is: [`app.py`](app.py)

This lightweight UI allows users to:

- View available Python files from HDFS  
- Preview scripts before execution  
- Select files to run via Spark  
- Set retry counts for failed jobs  
- View real-time execution results and statuses  

The interface uses the `ExecutionManager` class for backend logic.

### Installation

Install all required Python packages listed in the [`requirements.txt`](requirements.txt) file.

### Output Preview

You can the view the output screenshot here [DAS UI](DAS-UI.png)






## Conclusion

This project offers a reliable and user-friendly interface for managing and executing Python scripts stored in HDFS using Apache Spark.  
With real-time monitoring via Streamlit, execution tracking in MongoDB, and detailed logging support, the system ensures:

- Transparency in execution  
- Traceability of job status  
- Reliability across the entire workflow



# Setting Up PySpark on Mac with Jupyter Notebook

## 1. Install Homebrew (If not already installed)

Homebrew is a package manager for macOS. If you don't have it installed yet, run the following command in your terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 2. Install Java

PySpark requires Java. Install the latest version of OpenJDK using Homebrew:

```bash
brew install openjdk@17
```

Once installed, configure the environment variables in your shell configuration file (`~/.bash_profile`, `~/.zshrc`, etc.).

```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 17)
export PATH=$JAVA_HOME/bin:$PATH
```

Reload the shell configuration:

```bash
source ~/.zshrc  # or ~/.bash_profile
```

Check that Java is installed correctly:

```bash
java -version
```

## 3. Install Apache Spark

Use Homebrew to install Apache Spark:

```bash
brew install apache-spark
```

Verify the Spark installation by checking the version, make sure the version is >= 3.4:

```bash
spark-shell --version
```

## 4. Install Python and Create a Virtual Environment

Ensure that Python 3 is installed. You can install it via Homebrew if necessary:

```bash
brew install python
```

Create a virtual environment to isolate the PySpark installation:

```bash
python3 -m venv pyspark_env
source pyspark_env/bin/activate
```

## 5. Install PySpark and Jupyter Notebook in the Virtual Environment

With the virtual environment activated, install PySpark and Jupyter:

```bash
pip install pyspark
pip install notebook
```

## 6. Configure PySpark to Work with Jupyter

Create a configuration file to ensure that PySpark is correctly linked with Jupyter:

```bash
touch ~/.pyspark_env
```

Add the following lines to set the `PYSPARK_PYTHON` and `PYSPARK_DRIVER_PYTHON`:

```bash
export PYSPARK_PYTHON=python3
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS="notebook"
```

Then, source the environment variables:

```bash
source ~/.pyspark_env
```

## 7. Start Jupyter Notebook with PySpark

Launch Jupyter with PySpark by running the following command:

```bash
pyspark
```

This should open Jupyter Notebook in your browser, and you can now run PySpark code in the notebook environment.

## 8. Verify the Setup

Once inside Jupyter Notebook, verify that Spark is working by running:

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("pyspark-test").getOrCreate()

# Check Spark version
spark.version
```

If the Spark version is returned successfully, your setup is complete.

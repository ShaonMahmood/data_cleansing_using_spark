# Setting Up PySpark on Mac to run the notebook

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

With the virtual environment activated, install libraries from the requirements.txt file:

```bash
pip install -r requirements.txt
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

## 7. Data Preparation

Download the kaggle dataset from this link

[Card Transaction Dataset](https://www.kaggle.com/datasets/e47f88e5e8ce59c9598475a107d9a80ebc363a83859a59facb069b13a9001773)

After downloading, store it in a folder named data. Rename the downloaded file to **cc_transactions.json** to match with the name used inside notebook.

## 8. Start Jupyter Notebook with PySpark

Launch Jupyter with PySpark by running the following command:

```bash
pyspark
```

This should open Jupyter Notebook in your browser, and you can now run PySpark code in the notebook environment.

## 9. Run the notebook

Once inside Jupyter Notebook, open notebook file named "card_data_analysis.ipynb"

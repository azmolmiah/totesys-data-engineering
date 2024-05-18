## Directory Structure

`.github/workflows:`
- `main.yml`: The main workflow file that runs the tests and generates the coverage report.
- `deploy`: The main workflow to deploy and destroy terraform
  
`data_ingestion/`
- `ingestion_lambda.py`: Lambda function for data ingestion.
- `ingestion_schedule.tf`: Terraform script for scheduling the ingestion Lambda function.
- `cloudwatch/`: Directory for Cloudwatch logging and alerting scripts for the ingestion process.
- `tests/`: Directory for unit tests related to data ingestion.
  
`data_transformation/`
- `transformation_lambda.py`: Lambda function for data transformation.
- `transformation_trigger.tf`: Terraform script to trigger the transformation Lambda function.
- `cloudwatch/`: Directory for Cloudwatch logging and alerting scripts for the transformation process.
- `tests/`: Directory for unit tests related to data transformation.
  
`data_loading/`
- `loading_lambda.py`: Lambda function for loading data into the data warehouse.
- `loading_schedule.tf`: Terraform script for scheduling the loading Lambda function.
- `cloudwatch/`: Directory for Cloudwatch logging and alerting scripts for the loading process.
- `tests/`: Directory for unit tests related to data loading.
  
`terraform_structure/`
- `s3_buckets.tf`: Terraform script to create S3 buckets.
- `iam_roles.tf`: Terraform script to create IAM roles.
- `rds_instance.tf`: Terraform script to set up the RDS instance.
- `vpc.tf`: Terraform script to set up the VPC.
- `main.tf`: Main Terraform configuration file.
- `outputs.tf`: Terraform outputs.
- `variables.tf`: Terraform variables.
- `tests/`: Directory for unit tests related to infrastructure.
  
`dashboard/`
- `queries/`: Directory for SQL queries used in the Quicksight dashboard.
- `quicksight_setup.md`: Documentation for setting up Quicksight.
  
`utils/`
- `db_utils.py`: Utility functions for database operations.
- `s3_utils.py`: Utility functions for S3 operations.
- `logging_utils.py`: Utility functions for logging.
- `tests/`: Directory for unit tests for utility functions.
  
`Root Files`
- .env ? not sure if this will be handled by terraform env vars
- .gitignore: Gitignore file to exclude unnecessary files from version control.
- README.md: Project documentation.
- requirements.txt: Python dependencies.
- Dockerfile: Docker configuration.
-tox.ini: Configuration for Tox testing.

## Directory Structure

```plaintext
nc-totesys-az-version/
├── .github/
│   ├── workflows/
│   |   ├── deploy.yml
│   |   ├── main.yml
├── data_ingestion/
│   ├── __init__.py
│   ├── ingestion_lambda.py
│   ├── ingestion_schedule.tf
│   ├── cloudwatch/
│   │   ├── ingestion_logging.py
│   │   ├── cloudwatch_rules.tf
│   │   ├── cloudwatch_alerts.tf
│   └── tests/
│       ├── test_ingestion.py
│       ├── test_logging.py
│       └── test_utils.py
├── data_transformation/
│   ├── __init__.py
│   ├── transformation_lambda.py
│   ├── transformation_trigger.tf
│   ├── cloudwatch/
│   │   ├── transformation_logging.py
│   │   ├── cloudwatch_rules.tf
│   │   ├── cloudwatch_alerts.tf
│   └── tests/
│       ├── test_transformation.py
│       ├── test_logging.py
│       └── test_utils.py
├── data_loading/
│   ├── __init__.py
│   ├── loading_lambda.py
│   ├── loading_schedule.tf
│   ├── cloudwatch/
│   │   ├── loading_logging.py
│   │   ├── cloudwatch_rules.tf
│   │   ├── cloudwatch_alerts.tf
│   └── tests/
│       ├── test_loading.py
│       ├── test_logging.py
│       └── test_utils.py
├── infrastructure/
│   ├── s3_buckets.tf
│   ├── iam_roles.tf
│   ├── rds_instance.tf
│   ├── vpc.tf
│   ├── main.tf
│   ├── outputs.tf
│   ├── variables.tf
│   └── tests/
│       ├── test_infrastructure.py
├── dashboard/
│   ├── queries/
│   │   ├── sales_query.sql
│   │   ├── purchases_query.sql
│   │   ├── payments_query.sql
│   ├── quicksight_setup.md
├── utils/
│   ├── db_utils.py
│   ├── s3_utils.py
│   ├── logging_utils.py
│   └── tests/
│       ├── test_db_utils.py
│       ├── test_s3_utils.py
│       └── test_logging_utils.py
├── .env
├── .gitignore
├── Makefile
├── README.md
├── requirements.in
├── requirements.txt
├── Dockerfile
└── tox.ini ? Not sure the benifits of this
```

## Justification

This project structure is designed to be modular, organized, and maintainable, making it ideal for a complex data engineering and infrastructure project. Here are several reasons why this structure is beneficial:

#### 1. **Modularity**

- **Clear Separation of Concerns**: Each major component of the project (data ingestion, transformation, loading, infrastructure, utilities, dashboard) is placed in its own directory. This separation ensures that code related to specific functionalities is grouped together, making it easier to understand and manage.
- **Reusable Components**: Utility functions in the `utils` directory are shared across different parts of the project, promoting code reuse and reducing redundancy.

#### 2. **Maintainability**

- **Ease of Navigation**: The directory structure is intuitive, allowing developers to quickly find the relevant files and directories they need to work on. For example, all data ingestion-related files are in `data_ingestion/`, and all transformation-related files are in `data_transformation/`.
- **Isolated Tests**: Each functional area has its own `tests/` directory, making it easy to run unit tests and ensure code quality within specific modules. This isolation also helps in identifying and fixing issues more efficiently.

#### 3. **Scalability**

- **Component Expansion**: The modular structure allows for easy addition of new components or features. For example, if a new data processing step is needed, a new directory can be created without affecting the existing structure.
- **Infrastructure Management**: All Terraform scripts are organized within `terraform_structure/`, facilitating the management and deployment of infrastructure components. This separation also simplifies updates and maintenance of infrastructure code.

#### 4. **Collaboration**

- **Standardization**: Having a well-defined structure sets clear guidelines for team members, making collaboration easier. Everyone knows where to place new files and where to find existing ones.
- **Version Control**: The `.gitignore` file helps manage version control by excluding unnecessary files, ensuring that only relevant code and configurations are tracked.

#### 5. **Automation and CI/CD**

- **Automated Workflows**: The `.github/workflows/` directory contains CI/CD workflows (`main.yml` and `deploy.yml`), enabling automated testing, coverage reporting, and deployment. This integration ensures continuous integration and continuous delivery practices are followed.
- **Makefile Automation**: The `Makefile` provides commands for creating environments, installing dependencies, running tests, and checking code quality. This automation enhances productivity and ensures consistency in development practices.

#### 6. **Documentation and Configuration**

- **Comprehensive Documentation**: The `README.md` file provides essential project documentation, helping new developers get up to speed quickly.
- **Configuration Management**: Files like `requirements.txt`, `tox.ini`, and `Dockerfile` manage dependencies and testing configurations, ensuring a consistent development environment.

#### 7. **Environment Management**

- **Virtual Environment**: The `Makefile` includes targets for creating and managing a virtual environment, ensuring that dependencies are isolated and the development environment is reproducible.

#### Conclusion

This structure is designed to support the complexity and scale of a modern data engineering project. By promoting modularity, maintainability, scalability, collaboration, and automation, it provides a robust foundation for developing, testing, and deploying data processing and infrastructure components. This organized approach reduces the risk of errors, facilitates team collaboration, and enhances overall project quality.
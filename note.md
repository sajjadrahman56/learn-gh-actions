### **Introduction to GitHub Actions**

GitHub Actions allows you to automate tasks directly within your GitHub repository. A workflow is a series of automated steps defined in a `.yml` file, located in the `.github/workflows/` directory of your project.

### **Basic Requirements of a Workflow**

To create a valid workflow in GitHub Actions, there are a few essential components that must be present:

1. **Workflow Name (`name`)**:
   Every workflow should have a unique **name** that identifies it. This helps in distinguishing between different workflows in the repository.

2. **Trigger Event (`on`)**:
   The workflow must specify **when** it should run. This is defined under the `on` field. Common events include:
   - **push**: Triggered when you push code to the repository.
   - **pull_request**: Triggered when a pull request is opened or updated.
   - **workflow_dispatch**: Allows you to trigger a workflow manually.
   
3. **Job Definition (`jobs`)**:
   A workflow contains **jobs**, which are units of work executed in the workflow. Each job must have:
   - **Name of the job**: To identify the job within the workflow.
   - **OS environment (`runs-on`)**: This defines which operating system the job will run on. Popular options include `ubuntu-latest`, `windows-latest`, and `macos-latest`. Without specifying an OS, the workflow cannot run, as the steps need a virtual environment (like Ubuntu) to execute.

4. **Steps**:
   Each job is made up of **steps**, which are individual tasks to be executed in the workflow. These steps can include commands (like `echo`), GitHub-provided actions, or third-party actions.

---

### **1. First Workflow (`workflow.yml`)**

#### **Name: First Workflow**
This workflow runs automatically on a push to the `main` branch. It meets all the basic workflow requirements: it has a name, trigger, OS environment, and steps.

- **Name:**
  - `First Workflow` is the identifier for this workflow.

  ```yaml
  name: First Workflow
  ```

- **Trigger (`on`):**
  - The workflow will run when there’s a `push` to the `main` branch.

  ```yaml
  on:
    push:
      branches:
        - main
  ```

- **Jobs:**
  - The workflow defines one job called `first-workflow`.

  ```yaml
  jobs:
    first-workflow:
      runs-on: ubuntu-latest
  ```

  - The `runs-on` field specifies that the job will run on **Ubuntu** (the latest version). This is required to provide an environment where the steps will be executed.

- **Steps:**
  - There are two steps in this job:
    1. **First Step**: This step prints three messages to the console.
    2. **Second Step**: Prints a message indicating that this is the second step.

```yaml
    steps:
      - name: First Step
        run: |
          echo "this is first step"
          echo "Hello GH actions"
          echo "Do or Die"
          
      - name: Second Step
        run: |
          echo "yeah I am on the second step"
```

- **Summary**:
  This workflow runs automatically when code is pushed to the `main` branch and executes two steps that print messages in the console.

---

### **2. Manual Workflow (`manual-workflow.yml`)**

#### **Name: Manual Workflow**
This workflow can be triggered manually by a user from GitHub’s interface. It also satisfies the basic workflow requirements: name, trigger, OS, and steps.

- **Name:**
  - `Manual Workflow` is the name for this workflow.

  ```yaml
  name: Manual Workflow
  ```

- **Trigger (`on`):**
  - This workflow uses `workflow_dispatch`, which means it can be triggered manually via the GitHub Actions interface.

  ```yaml
  on:
    workflow_dispatch:
  ```

- **Jobs:**
  - The workflow defines a job called `first-workflow`, which also runs on the latest version of Ubuntu (`ubuntu-latest`).

  ```yaml
  jobs:
    first-workflow:
      runs-on: ubuntu-latest
  ```

- **Steps:**
  - There is only one step in this workflow, which prints three messages to the console.

  ```yaml
    steps:
      - name: First Step
        run: |
          echo "this is first step"
          echo "Hello GH actions"
          echo "Do or Die"
  ```

- **Summary**:
  This workflow can be started manually via the GitHub interface and prints messages to the console when executed.

---

### **Key Points to Remember:**

- **Basic Workflow Structure:**
  1. **Name**: Each workflow needs a name.
  2. **Trigger (`on`)**: Workflows must have a trigger event (like `push` or `workflow_dispatch`).
  3. **Jobs and OS Environment (`runs-on`)**: Each job must specify an OS environment to run on, such as `ubuntu-latest`. Without this, the workflow won’t be able to run.
  4. **Steps**: Define the individual tasks that will be executed in the job.

- **Differences Between the Two Workflows:**
  - The **First Workflow** is triggered automatically on a push to the `main` branch, whereas the **Manual Workflow** is triggered manually.

---

### Step 2: Detect Vulnerabilities in a Pull Request

To see how Code Scanning works, we will introduce two different vulnerabilities into the `routes.py` file to trigger alerts.

#### ⌨ Activity: Create vulnerabilities

1. In the top navigation, select the **Code** tab.

2. Navigate to the `server` folder and select the `routes.py` file.

3. In the top right of the preview, click the **Edit** button.

4. Navigate to about **line 16** and modify it to the following:

   ```python
   query = "SELECT * FROM books WHERE name LIKE '%" + name + "%'"
   ```

5. A few lines below, add a second vulnerability by inserting the following code:

   ```python
   filename = request.args.get("file")
   with open("/var/data/" + filename, "r") as f:
       data = f.read()
   ```

6. Above the editor in the top-right, click the **Commit changes...** button. In the prompt window, select the radio button for the **Create a new branch** option. DO NOT commit to the main branch.

7. Click the **Propose changes** option and then click **Create pull request**. Use the following branch name:

   ```
   learning-codeql
   ```

8. On the new page, below the pull request description, click the **Create pull request** button.

#### ⌨ Activity: Review pull request

1. If needed, navigate to the newly created pull request from the previous activity.

2. Scroll to the bottom of the pull request and locate the check named **CodeQL**. This is the analysis job scanning the proposed code changes in the pull request.

3. If the job is still running, wait a few minutes for it to complete.

4. Review the results of the analysis in the pull request comments.

   * You should see two alerts: one for a SQL injection and one for a path traversal vulnerability.
   * Some alerts may include suggestions with the option to apply a fix.

5. Tip: Clicking the **Show paths** link will provide additional insights about the alert's data flow from user input (source), through the application, and when it is acted on (sink).

#### ⌨ Activity: View the CodeQL scanning logs

1. In the top navigation, select the **Actions** tab.
2. In the left navigation, select the **CodeQL** entry to filter the workflow runs.
3. Click on the workflow run with the name **PR #X** (where X is the pull request number) to open a page with more details.
4. Expand the run jobs by clicking **Show all jobs**, then click on the **Analyze (python)** entry.
5. Find the analysis entry and review the logs.
6. With the pull request started and CodeQL scan finished, Mona will check your progress and share the next steps.

### Workflow for JetBrains youtrack for creating extra issues
#### Description
The workflow creates two extra issues for functional and unit tests upon an issue creation. The extra issues are being created only for issues with type "Bug" or "Feature". The extra issues have type "Meta Issue"


```
rule Create Unit and Functional Tests Issues as Subtasks 
 
when becomesReported() { 
  if (issue.Type == {Feature} || issue.Type == {Bug}) { 
    var functionalIssue = loggedInUser.createNewIssue(project.shortName); 
    var unitIssue = loggedInUser.createNewIssue(project.shortName); 
    functionalIssue.Type = {Meta Issue}; 
    functionalIssue.summary = "Functional tests for " + issue.summary; 
    functionalIssue.description = "Create functional tests for " + issue.getUrl(); 
    functionalIssue.subtask of.add(issue); 
    unitIssue.Type = {Meta Issue}; 
    unitIssue.summary = "Unit tests for " + issue.summary; 
    unitIssue.description = "Create unit tests for " + issue.getUrl(); 
    unitIssue.subtask of.add(issue); 
  } 
}
```
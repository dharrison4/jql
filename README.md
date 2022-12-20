# jql

My favorite JQL queries

---

## Omit 

If the main body of the ticket has these keywords, don't return.

> Any MHC (project) tickets that have the word `printer` but not the word `parking`

`created >= -7d AND project = MHC AND text ~ "printer" AND NOT text ~ "parking"`

---

- Original JQL article at the [source](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/).
- Inspired by [this by jscanzoni](inspired by https://github.com/jscanzoni/jql).

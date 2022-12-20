# jql

My favorite JQL queries. 

JQL can be quite forgiving so I will put down a couple derivatives as I think of them.

---

## Omit 

If the main body of the ticket has these keywords, don't return.

> Any MHC (project) tickets that have the word `printer` but not the word `parking`.

```
text ~ printer AND NOT text ~ parking        # notice the lack of quotations around the keyword. If there was a space there, you should use quotations
text ~ "printer" AND NOT text ~ "parking"    # does the same as above
```

---

- Original JQL article at the [source](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/).
- Inspired by [this by jscanzoni](inspired by https://github.com/jscanzoni/jql).

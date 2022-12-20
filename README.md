# jql

My favorite JQL queries. 

JQL can be quite forgiving so I will put down a couple derivatives as I think of them.

---

## Omit 

If the main body of the ticket has these keywords, don't return.

> Any tickets that have the word `printer` but not the word `parking`.

```
text ~ printer AND NOT text ~ parking        # notice the lack of quotations around the keyword. If there was a space there, you should use quotations
text ~ "printer" AND NOT text ~ "parking"    # does the same as above
text ~
```

## Multiple keywords

It looks like `"konica printer"` should be processed differently to `"konica" AND "printer"`, but not in JQL. If there is more than one word in the quotations, it does not specifically look for only instances where the two words are together. Demonstration:

> Any tickets that have the words `konica` and `printer` anywhere in them
 ```
 text ~ "printer" AND text ~ "konica"
 text ~ "printer konica"                      #no difference!
 ```
 
 ## More to come
 ### as I think of them

---

- Original JQL article at the [source](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/).
- Inspired by [this by jscanzoni](https://github.com/jscanzoni/jql).

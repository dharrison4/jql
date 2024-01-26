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

### Specific keywords

You can search for specific and non-specific (fuzz) text. To continue on from the Konica Printer example above:

> Any tickets that have the words 'konica printer', together, specifically in this order.
> ```
> text ~ "\"konica printer\""
> ```

the `\` is not an error in GitHub formatting, it is literally what I have to use in a JQL search to include quotations for a string. `text ~ kinda search terms here` vs `text ~ "these exact search terms here"`
 
 ## All tickets that I have, unfinished
 ```
 assignee in (currentUser()) AND status not in (Done, Completed, Closed)
 ```
 You can also add 

## any improperly categorized tickets

### no dept & no sub-dept
```
updated >= startofyear() #arbitrary 
AND
    ("Department Queue" is EMPTY OR "Department Queue" in cascadeOption(11307) 
    AND
    "Department Queue" not in cascadeOption(11307, 11541) 
    AND
    "Department Queue" not in cascadeOption(11307, 11308) 
    AND
    "Department Queue" not in cascadeOption(11307, 14665) 
    AND
    "Department Queue" not in cascadeOption(11307, 14178) 
    AND
    "Department Queue" not in cascadeOption(11307, 15115) 
    AND
    "Department Queue" not in cascadeOption(11307, 15091) 
    AND
    "Department Queue" not in cascadeOption(11307, 15379)) 
AND
 (project = MHC OR project = HAR) 
AND
 "Request Type" != "Laptop loan request (HAR)" 

ORDER BY Updated ASC
```
The above filter JQL will grab any MHC or HAR tickets that don't have a department, or don't have a complete department. 

E.g. `11307, 11308` - this is `Client Services - Classroom support`

---
 
## More to come
### as I think of them

---

- Original JQL article at the [source](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/).
- Inspired by [this by jscanzoni](https://github.com/jscanzoni/jql).

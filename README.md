# jql

My favorite JQL queries. 

JQL can be quite forgiving so I will put down a couple derivatives as I think of them.

Jira updated how JQL queries are composed. It seems to be entirely aestetic instead of functional. Because of this, any images on this page may be outdated.

---

## Keeping up to date with current events

Let's say, for example, I work in tech support but I enjoy looking at CyberSecurity-related tickets so I can learn more about 1) MacEwan's IT infrastructure, 2) MacEwan's security and privacy policies, 3) trends for cybersecurity from the POV of support desk (is something trending?) and 4) the field of cybersecurity in general. _Always be learning_.

1. Assigned to the current user
   - `assignee = currentUser()`
2. Created this year
   - `created >= StartOfYear()`
3. Keyword list in `text` or `summary` fields
   - `text ~ "approx match in the text field"`
   - `summary ~ "approx match in the ticket title field"`
   - the list:
     - secur*
     - cyber*
     - cybersec*
     - hack*
     - phish*
     - compromise
     - malware
     - malicious
     - breach
     - vulnerab
     - fire*wall
     - encrypt*
     - incident response
     - authenticat*
     - ransom*
     - MFA
     - 2FA
     - Multi*factor
     - 2*factor
     - DDOS
     - security awareness training

```
(text~"security" OR text~"secure" OR text~"cyber" OR text~"cybersecurity" OR text~"cybersec" OR text~"hack" OR text~"phish" OR text~"phishing" OR text~"compromise" OR text~"malware" OR text~"breach" OR text~"vulnerable" OR text~"vulnerability" OR text~"firewall" OR text~"fire wall" OR text~"encryption" OR text~"encrypt" OR text~"encrypted" OR text~"incident response" OR text~"authentication" OR text~"authenticate" OR text~"ransom" OR text~"ransomware" OR text~"MFA" OR text~"2FA" OR text~"Multi-factor" OR text~"2-factor" OR text~"DDOS" OR text~"security awareness training" OR summary~"security" OR summary~"secure" OR summary~"cyber" OR summary~"cybersecurity" OR summary~"cybersec" OR summary~"hack" OR summary~"phish" OR summary~"phishing" OR summary~"compromise" OR summary~"malware" OR summary~"breach" OR summary~"vulnerable" OR summary~"vulnerability" OR summary~"firewall" OR summary~"fire wall" OR summary~"encryption" OR summary~"encrypt" OR summary~"encrypted" OR summary~"incident response" OR summary~"authentication" OR summary~"authenticate" OR summary~"ransom" OR summary~"ransomware" OR summary~"MFA" OR summary~"2FA" OR summary~"Multi-factor" OR summary~"2-factor" OR summary~"DDOS" OR summary~"security awareness training") 
AND 
assignee = currentUser()
AND
created >= startOfYear()

order by Updated DESC, statusCategory ASC
```

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
 assignee in currentUser() AND status not in (Done, Completed, Closed)
 ```
...#or...
 ```
 assignee in currentUser() AND statusCategory != Done
 ```

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
The above filter JQL will grab any MHC or HAR tickets that don't have a department, or don't have a _complete_ department. 

E.g. `11307, 11308` - this is `Client Services - Classroom support`

---
 
## More to come
### as I create/improve them

---

- Original JQL article at the [source](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/).
- Inspired by [this by jscanzoni](https://github.com/jscanzoni/jql).

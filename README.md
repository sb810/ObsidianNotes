# Daily Notes
```dataview
Table
From #dailynote where file.name != "Daily notes template"
sort date
```

# purchases
```dataview
Task where price > 0 and completed
Group by file.link
```


# [[Subscriber Space]] tasks
```dataview
TABLE status, completed, due, urgent
FROM "Studio XP/Subscriber Space"
SORT status
```

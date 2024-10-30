
---

## 说明
> 任务列表可以通过dataview语法 也可以通过tasks插件获取

## 所有未完成的任务

````ad-col2
title: ### 展开所有未完成的任务和过滤含有关键字的任务
```dataviewjs
//filter输入要过滤的任务关键字
let filter ="" 
//noflod 输入要排除的文件夹
let noflod ='!"01-Template"'
const groups = dv.pages(noflod).filter(p => p.file.folder != "").groupBy(p => p.file.folder.split("/")[0])
for (let group of groups) {
let tasks=dv.pages(`"${group.key}"`).where(t => { return t.file.name != "" }).file.tasks.where(t => t.text.includes(filter) && !t.completed)
if(tasks.length>0)
dv.header(3, group.key);
dv.taskList(tasks,1)
}
```
````

```ad-tip
可以通过输入@ 快速输入日期 支持自然语言格式比如
`@today` 今天
`@in 3 days`  3天后
`@3 days ago`  3天前
```

## 任务收集【tasks】

````ad-caution
title: 过期的任务
```tasks
not done
due before  today
path does not include "01-Template"
short mode
```
````

````ad-check
title: 今天要完成的任务
```tasks
not done
due on  today 
path does not include "01-Template"
short mode
```
````

> [!CHECK] 3天内要完成的任务
> ```tasks
not done 
due after today
due before in 3 days 
path does not include "01-Template"
short mode
>```

````ad-todo
title: 未两周要完成的任务
```tasks
not done 
due after today
due before in two weeks
path does not include "01-Template"
short mode
```
````

## 任务收集【dataview】

````ad-caution
title: 过期的任务
```dataview
task
from !"01-Template"
where !completed
AND due <= date(today)
sort file.cday asc
```
````

````ad-check
title: 今天要完成的任务
```dataview
task
from !"01-Template"
where !completed
AND due = date(today)
sort file.cday asc
```
````

> [!CHECK] 3天内要完成的任务
> ```dataview
task
where file.path = this.file.path 
where !completed
WHERE due > date(today) + dur(1 days)
WHERE due <= date(today) + dur(3 days)
sort file.cday asc
>```

````ad-todo
title: 六月任务
```dataview
task
where file.path = this.file.path 
where !completed
WHERE due >= date(2022-06-01) 
WHERE due <= date(2022-06-31) 
sort file.cday asc
```
````

## 任务举例

- [ ] 这是一个任务带标签的内容 #紧急任务
- [ ] 这是一个自定义任务 #测试 

````ad-example
title: dvjs版本查看超期任务
```dataviewjs
function overdue(t) {
  let dValidate = moment(t.text, 'YYYY-MM-DD', true);
  let d = moment(t.text, 'YYYY-MM-DD');
  let containsValidDate = dValidate._pf.unusedTokens.length==0;
  let isOverdue = d.diff(moment()) <= 0;
  return (containsValidDate && isOverdue);
}
dv.taskList(dv.pages("").file.tasks.where (t => overdue(t)).where (t => !t.completed))
```
````

## 查询带自定义字段的任务
````ad-flex
```dataview
TASK 
where file.path = this.file.path  
WHERE Group1 
FLATTEN Group1 
GROUP BY Group1 
```
````

### 查询带标签的任务
```dataview
task
WHERE contains(tags, "#紧急任务")
```

--- 

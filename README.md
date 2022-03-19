# Database-HW8

6310545426 Siratee Kittiwitchaowakul

## 5
Create MongoDB database with following information
```
[
  {"name":"Ramesh","subject":"maths","marks":87},
  {"name":"Ramesh","subject":"english","marks":59},
  {"name":"Ramesh","subject":"science","marks":77},
  {"name":"Rav","subject":"maths","marks":62},
  {"name":"Rav","subject":"english","marks":83},
  {"name":"Rav","subject":"science","marks":71},
  {"name":"Alison","subject":"maths","marks":84},
  {"name":"Alison","subject":"english","marks":82},
  {"name":"Alison","subject":"science","marks":86},
  {"name":"Steve","subject":"maths","marks":81},
  {"name":"Steve","subject":"english","marks":89},
  {"name":"Steve","subject":"science","marks":77},
  {"name":"Jan","subject":"english","marks":0,"reason":"absent"}  
]
```

** The collection name is `Users` **

### 1. Find the total marks for each student across all subjects.

```py
db.Users.aggregate(
    [
      {
        $group: {
          _id: "$name",
          SumScore: {
            $sum: "$marks"
          }
        }
      }
    ]
  )
```
![Screen Shot 2565-03-19 at 15 11 11](https://user-images.githubusercontent.com/25188615/159113944-f2328f8c-11e6-4a61-9a20-533512841487.png)


### 2. Find the maximum marks scored in each subject.

```py
db.Users.aggregate(
    [
      {
        $group: {
          _id: "$subject",
          MaxScore: {
            $max: "$marks"
          }
        }
      }
    ]
  )
```
![Screen Shot 2565-03-19 at 15 38 23](https://user-images.githubusercontent.com/25188615/159114128-e0d6ac38-6b41-4a8b-9a2a-605b94c976c5.png)



### 3. Find the minimum marks scored by each student.

```py
db.Users.aggregate(
    [
      {
        $group: {
          _id: "$name",
          MinScore: {
            $min: "$marks"
          }
        }
      }
    ]
  )
```
![Screen Shot 2565-03-19 at 15 11 42](https://user-images.githubusercontent.com/25188615/159113986-a3775403-0f67-4265-94a0-c273f8244e1f.png)


### 4. Find the top two subjects based on average marks.

```py
db.Users.aggregate(
    [
      {
        $group: {
          _id: "$subject",
          avg: {
            $avg: "$marks"
          }
        },
      },
      {
        $sort: {
          avg: -1
        }
      },
      {
        $limit: 2
      }
    ]
  )
```
![Screen Shot 2565-03-19 at 15 37 33](https://user-images.githubusercontent.com/25188615/159114096-f6cd9168-8481-4ef0-8682-577518a57ebe.png)



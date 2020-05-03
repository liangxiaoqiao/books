##### 1. 分组柱状图
```python
def pandas_bar_graph():
    users = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
    users.sort_values(by='2017', inplace=True, ascending=False)
    users.plot.bar(x='Name', y=['2016', '2017'],
                   color=['red', 'green'], title="This is first graph")
    # plt.xticks(rotation=50)
    plt.xlabel('Names')
    plt.ylabel('Scores')
    plt.title('Mat plot Graph', fontweight='bold')
    ax = plt.gca()
    ax.set_xticklabels(users.Name, rotation=45, ha='right')
    plt.gcf().subplots_adjust(right=0.8, bottom=0.1)
    plt.show()
```

##### 2.叠加柱状图 横向
```python
def pandas_add_grp():
    users = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
    users['MyTotal'] = users['2016'] + users['2017'] + users['2018']
    users.sort_values(by='MyTotal', ascending=True, inplace=True)
    # users.plot.bar(x='Name', y=['2016', '2017', '2018'], stacked=True) # 竖直
    users.plot.barh(x='Name', y=['2016', '2017', '2018'], stacked=True)  # 水平
    plt.title("Three Graph", fontweight='bold')
    # plt.gca().set_xticklabels(users.Name, rotation=45, ha='right')
    plt.xlabel("Names", fontsize=10)
    plt.ylabel("Scores", fontsize=10)
    plt.show()
```

##### 3.饼图
```python
def pandas_pie():
    users = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='Name')
    users['MyTotal'] = users['2016'] + users['2017'] + users['2018']
    users['2017'].plot.pie(counterclock=False)
    plt.show()
```

##### 4. 散点图

```python
pb.plot.scatter(x="Name",y="Year")
```
##### 5. 直方图
```python
homes['col'].plot.hist(bins=100) 
```

##### 6. 密度图
```python
homes['col'].plot.kde()
```

##### 7. 透视图
```python
def pandas_pivot():
    df = pd.read_excel("c:\\test\\create_all.xlsx")
    pt1 = df.pivot_table(index="School", columns="Grade", values="2017", aggfunc=np.sum)
    # print(pt1)

    groups = df.groupby(['School', "Grade"])
    s = groups['2017'].sum()
    r = groups['2019'].sum()
    t = groups['2020'].sum()

    pt2 = pd.DataFrame({"Total 2017": s, "Total 2019": r, "Total 2020": t})
    print(pt2)
```

##### 图
```python
# 柱状图
users.plot.bar(x='Name', y=['2016', '2017'],
                   color=['red', 'green'], title="This is first graph")
#竖直 叠加柱状图
users.plot.bar(x='Name', y=['2016', '2017', '2018'], stacked=True)
#水平 叠加柱状图
users.plot.barh(x='Name', y=['2016', '2017', '2018'], stacked=True)

# 折线图
users.plot(y=['2016', '2017', '2018'], color=['red', 'green', 'blue'])
# 叠加区域图
users.plot.area(y=['2016', '2017', '2018'], color=['red', 'green', 'blue'], stacked=True)
```

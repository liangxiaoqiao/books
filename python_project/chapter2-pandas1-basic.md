##### 1. 创建Excel
```python
def create_20162017():
    ids = []
    names = []
    fields = []
    fields2 = []
    fields3 = []
    bools = []
    for i in range(0, 20):
        ids.append(i + 1)
        fields2.append(random.randint(10, 100))
        fields.append(fields2[-1] + random.randint(-5, 5))
        fields3.append(random.randint(5, 20))
        names.append(ranstr(random.randint(2, 8 if fields2[-1] > 70 else 20)))
        bools.append("Yes" if i % 2 == 0 else "No")
    s1 = pd.Series(fields, index=ids, name="2016")
    s2 = pd.Series(fields2, index=ids, name="2017")
    s3 = pd.Series(fields3, index=ids, name="2018")
    sbool = pd.Series(bools, index=ids, name='Bool')
    sname = pd.Series(names, index=ids, name="Name")
    stotal = pd.Series([], name='Total')
    df = pd.DataFrame(
        {"ID": ids, sname.name: sname, sbool.name: sbool, s1.name: s1, s2.name: s2, s3.name: s3, stotal.name: stotal})
    df.set_index('ID', inplace=True)
    df.to_excel("c:\\test\\create_20162017.xlsx")
    print(df)
```

##### 2. 创建行列数据
```python
def pandas_series():
    d = {'x': 1, 'y': 100, 'z': 200}
    s1 = pd.Series(d)
    print(s1)
    print_se()

    L1 = [100, 200, 300]
    s1 = pd.Series(L1, index=['X', 'Y', 'Z'])
    df = pd.DataFrame(s1)
    print(df)
    print_se()
```

##### 3. 读取的时候skip
```python
def pandas_skip_apply():
    df = pd.read_excel("c:\\test\\create_20162017.xlsx", skiprows=0, usecols='B,D')
    print(df)
    print_se()
    df = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
    df['2017'].at[2] = 100
    df.at[3, '2017'] = 200
    df['Total'] = df['2016'] * 2 + df['2017']
    df['Total'] = df['Total'].apply(lambda x: x / 100)
    print(df)
    print_se()
```

##### 4. 排序
```python
def pandas_sort():
    df = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
    df.sort_values(by=['Bool', '2016'], inplace=True, ascending=(False, False))
    print(df)
    print_se()
```

##### 5. 过滤
```python
def pandas_filter():
    df = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
    df = df.loc[df['2016'].apply(lambda x: x >= 50)].loc[df.Bool.apply(lambda x: x == 'Yes')]
    print(df)
```

##### 6. 分组柱状图
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

##### 7.叠加柱状图 横向
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

##### 8.饼图
```python
def pandas_pie():
    users = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='Name')
    users['MyTotal'] = users['2016'] + users['2017'] + users['2018']
    users['2017'].plot.pie(counterclock=False)
    plt.show()
```
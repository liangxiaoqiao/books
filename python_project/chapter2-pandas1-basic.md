1. ##### 创建Excel
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

2. ##### 创建行列数据
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

3. ##### 读取的时候skip
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

4. ##### 排序
    ```python
    def pandas_sort():
        df = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
        df.sort_values(by=['Bool', '2016'], inplace=True, ascending=(False, False))
        print(df)
        print_se()
    ```

5. ##### 过滤
    ```python
    def pandas_filter():
        df = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
        df = df.loc[df['2016'].apply(lambda x: x >= 50)].loc[df.Bool.apply(lambda x: x == 'Yes')]
        print(df)
    ```

1. ##### 条件格式

    ```python
    # applymap作用每一个单元格
    # apply分别作用域每一列
    def pandas_condition():
        users = pd.read_excel("c:\\test\\create_20162017.xlsx", index_col='ID')
        users = users.style.applymap(less, subset=['2016', '2017', '2018']) \
            .apply(more, subset=['2016', '2017', '2018'])
        print(type(users))
        users.to_excel("c:\\test\\test2.xlsx")
    ```
1. ##### Join多表联合
    ```python
    def pandas_join():
        student16 = pd.read_excel("c:\\test\\create_161718.xlsx")
        student20 = pd.read_excel("c:\\test\\create_1920l.xlsx")
        tables = student16.merge(student20, how="left", left_on="Name", right_on="Name").fillna(0)
        print(tables)
    ```
1. ##### 校验
    ```python
    def score_validation(row):
    if not 0 <= row['2016'] <= 30:
        print(f'#{row.ID}\tstudents "2016" has an invalid score {row["2016"]}')

    def pandas_validate():
        students = pd.read_excel("c:\\test\\create_161718.xlsx")
        students.apply(score_validation, axis=1)
    ```
1. ##### 列分割
    ```python
    def pandas_col_split():
        students = pd.read_excel("c:\\test\\create_all.xlsx")
        df = students['Name'].str.split(expand=True)
        students['First Name'] = df[0]
        students['Last Name'] = df[1]
        print(students)
    ```
1. ##### 统计
    ```python
    def pandas_calc():
        students = pd.read_excel("c:\\test\\create_all.xlsx")
        sum2016 = students["2016"].sum()
        mean2017 = students["2017"].mean()
        print(sum2016)
        print(mean2017)
        df = students.mean(axis=0)
        print(df)
    ```
1. ##### 去重
    ```python
    def pandas_duplicate():
        pd.options.display.max_columns = 999
        students = pd.read_excel("c:\\test\\create_all.xlsx")
        # students.drop_duplicates(subset="2016", keep="first", inplace=True)
        dups = students.duplicated(subset="2016")
        dups = dups[dups]
        print(dups)
        s2 = pd.Series([1, 2, 3, 4, 5, 6, 7, 8])
        s2 = s2[s2.values > 5]  # 等价 s2[s2 > 5]   s2.values 为np.ndarray
        print(s2)
    ```
7. ##### 行列操作
    ```python
    def pandas_row_col_handle():
        df1 = pd.read_excel("c:\\test\\create_20162017.xlsx")
        df2 = pd.read_excel("c:\\test\\create_20162017_2.xlsx")
        # 合并 按行添加到最后一行右边
        students = df1.append(df2)
        # 重建索引
        students.reset_index(drop=True)
        # 增
        alex = pd.Series({"ID": 100, "Name": "Alex", "Bool": "True", "2016": 99, "2017": 98, "2018": 90})
        students = students.append(alex, ignore_index=True)
        alex2 = pd.Series({"ID": 100, "Name": "Alex2", "Bool": "True", "2016": 99, "2017": 98, "2018": 90})
        students = students.loc[:10].append(alex2, ignore_index=True).append(students[10:])
        # 删
        students.drop(index=range(0, 5), inplace=True)
        students.drop(index=students[0:5].index, inplace=True)
        students = students.reset_index(drop=True)
        # 改
        students.at[0, "2016"] = 150
        students.iloc[1] = alex2
        students['Total'] = students['2016'] + students['2017'] + students['2018']
        # filter
        filter_index = students.loc[students['Name'].apply(lambda name: name == 'Iso')].index
        students.drop(index=filter_index, inplace=True)

        # Col
        # 合并 按列添加到右侧
        # students = pd.concat([df1, df2], axis=1)
        students = pd.concat([df1, df2])  # 竖直添加
        # 增
        students['Age'] = 18
        students.insert(1, column='Index1', value=5)
        # 删
        students.drop(columns=['Bool', 'Age'], inplace=True)
        # 改
        students.rename(columns={"Index1": "INDEX1", "Name": "NAME"}, inplace=True)
        for i in range(5, 10):
            students['NAME'].at[i] = np.nan
        # drop
        students.dropna(subset=['NAME'], inplace=True)
        print(students)
    ```


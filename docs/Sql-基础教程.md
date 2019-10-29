# sql 基础教程

Created By: onesfish onesfish
Last Edited: Oct 25, 2019 11:26 AM

-- 创建数据库 shop
    CREATE DATABASE shop; 
    
    -- 创建表 Product 
    CREATE TABLE Product
    (
      product_id CHAR(4) NOT NUll,
      product_name VARCHAR(100) NOT NULL,
      product_type VARCHAR(32) NOT NULL,
      sale_price INTEGER, 
      purchase_price INTEGER,
      regist_date DATE,
      PRIMARY KEY (product_name)
    );
    
    -- 删除表 Product
    DROP TABLE Product;
    
    -- 给 Product 表 添加列
    ALTER TABLE Product ADD COLUMN product_name_pinyin VARCHAR(100);
    
    -- 给 Product 表 删除列
    ALTER TABLE Product DROP COLUMN product_name_pinyin;
    
    -- 给 Product 表 插入数据
    BEGIN TRANSACTION;
    INSERT INTO Product VALUES ('0001', 'T恤杉' ,'衣服', 1000, 500, '2009-09-20');
    INSERT INTO Product VALUES ('0002', '打孔器', '办公用品', 500, 320, '2009-09-11');
    INSERT INTO Product VALUES ('0003', '运动T恤', '衣服', 4000, 2800, NULL);
    INSERT INTO Product VALUES ('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20');
    INSERT INTO Product VALUES ('0005', '高压锅', '厨房用具', 6800, 5000, '2009-01-15');
    INSERT INTO Product VALUES ('0006', '叉子', '厨房用具', 500, NULL, '2009-09-20');
    INSERT INTO Product VALUES ('0007', '擦菜板', '厨房用具', 880, 790, '2008-04-28');
    INSERT INTO Product VALUES ('0008', '圆珠笔', '办公用品', 100, NULL, '2009-11-11');
    COMMIT;
    
    -- 变更表名,更改表名. 将 Product 改为 Poduct (SQL 标准中没有 RENAME)
    ALTER TABLE Product RENAME TO Poduct;
    
    -- 查询指定列
    SELECT
    product_id,
    product_name,
    purchase_price
    FROM
    Product;
    
    -- result
    product_id | product_name | purchase_price 
    ------------+--------------+----------------
     0001       | T恤杉        |            500
     0002       | 打孔器       |            320
     0003       | 运动T恤      |           2800
     0004       | 菜刀         |           2800
     0005       | 高压锅       |           5000
     0006       | 叉子         |               
     0007       | 擦菜板       |            790
     0008       | 圆珠笔       |               
    (8 行记录)
    
    -- 查询全部列, 查询所有列
    SELECT * FROM Product;
    
    -- result
    product_id | product_name | product_type | sale_price | purchase_price | regist_date 
    ------------+--------------+--------------+------------+----------------+-------------
     0001       | T恤杉        | 衣服         |       1000 |            500 | 2009-09-20
     0002       | 打孔器       | 办公用品     |        500 |            320 | 2009-09-11
     0003       | 运动T恤      | 衣服         |       4000 |           2800 | 
     0004       | 菜刀         | 厨房用具     |       3000 |           2800 | 2009-09-20
     0005       | 高压锅       | 厨房用具     |       6800 |           5000 | 2009-01-15
     0006       | 叉子         | 厨房用具     |        500 |                | 2009-09-20
     0007       | 擦菜板       | 厨房用具     |        880 |            790 | 2008-04-28
     0008       | 圆珠笔       | 办公用品     |        100 |                | 2009-11-11
    (8 行记录)
    
    -- 给列 设置别名
    SELECT
    product_id AS id,
    product_name AS name,
    purchase_price AS price
    FROM
    Product;
    
    -- result
    id  |  name   | price 
    ------+---------+-------
     0001 | T恤杉   |   500
     0002 | 打孔器  |   320
     0003 | 运动T恤 |  2800
     0004 | 菜刀    |  2800
     0005 | 高压锅  |  5000
     0006 | 叉子    |      
     0007 | 擦菜板  |   790
     0008 | 圆珠笔  |      
    (8 行记录)
    
    -- 给列 设置别名 (中文别名)
    SELECT
    product_id AS "商品编号",
    product_name AS "商品名称",
    purchase_price AS "进货单价"
    FROM
    Product;
    
    -- result
    商品编号 | 商品名称 | 进货单价 
    ----------+----------+----------
     0001     | T恤杉    |      500
     0002     | 打孔器   |      320
     0003     | 运动T恤  |     2800
     0004     | 菜刀     |     2800
     0005     | 高压锅   |     5000
     0006     | 叉子     |         
     0007     | 擦菜板   |      790
     0008     | 圆珠笔   |         
    (8 行记录)
    
    -- 查询常数
    SELECT
    '商品' AS string,
    38 AS number,
    '2009-02-24' AS date,
    product_id,
    product_name
    FROM
    Product;
    
    -- result
    string | number |    date    | product_id | product_name 
    --------+--------+------------+------------+--------------
     商品   |     38 | 2009-02-24 | 0001       | T恤杉
     商品   |     38 | 2009-02-24 | 0002       | 打孔器
     商品   |     38 | 2009-02-24 | 0003       | 运动T恤
     商品   |     38 | 2009-02-24 | 0004       | 菜刀
     商品   |     38 | 2009-02-24 | 0005       | 高压锅
     商品   |     38 | 2009-02-24 | 0006       | 叉子
     商品   |     38 | 2009-02-24 | 0007       | 擦菜板
     商品   |     38 | 2009-02-24 | 0008       | 圆珠笔
    (8 行记录)
    
    -- 从结果中删除重复行
    SELECT DISTINCT
    product_type
    FROM
    Product;
    
    -- result
    product_type 
    --------------
     衣服
     办公用品
     厨房用具
    (3 行记录)
    
    -- 从结果中删除重复行 (NULL 数据也会被合并成一条)
    SELECT DISTINCT
    purchase_price
    FROM
    Product;
    
    -- result
    purchase_price 
    ----------------
                   
                320
                500
               2800
               5000
                790
    (6 行记录)
    
    -- WHERE 子局
    SELECT
    product_name,
    product_type
    FROM
    Product
    WHERE
    product_type = '衣服';
    
    -- result
    product_name | product_type 
    --------------+--------------
     T恤杉        | 衣服
     运动T恤      | 衣服
    (2 行记录)
    
    -- 算数运算符
    SELECT
    product_name,
    sale_price,
    sale_price * 2 AS "sale_price_x2"
    FROM
    Product;
    
    -- result
    product_name | sale_price | sale_price_x2 
    --------------+------------+---------------
     T恤杉        |       1000 |          2000
     打孔器       |        500 |          1000
     运动T恤      |       4000 |          8000
     菜刀         |       3000 |          6000
     高压锅       |       6800 |         13600
     叉子         |        500 |          1000
     擦菜板       |        880 |          1760
     圆珠笔       |        100 |           200
    (8 行记录)
    
    -- 比较运算符 (不等于)
    SELECT
    product_name,
    product_type
    FROM
    Product
    WHERE
    sale_price <> 500;
    
    -- result
    product_name | product_type 
    --------------+--------------
     T恤杉        | 衣服
     运动T恤      | 衣服
     菜刀         | 厨房用具
     高压锅       | 厨房用具
     擦菜板       | 厨房用具
     圆珠笔       | 办公用品
    (6 行记录)
    
    -- 计算表达式
    SELECT
    product_name,
    sale_price,
    purchase_price
    FROM
    Product
    WHERE
    sale_price - purchase_price >= 500;
    
    -- result
    product_name | sale_price | purchase_price 
    --------------+------------+----------------
     T恤杉        |       1000 |            500
     运动T恤      |       4000 |           2800
     高压锅       |       6800 |           5000
    (3 行记录)
    
    -- 查询空 NULL
    SELECT
    product_name,
    purchase_price
    FROM
    Product
    WHERE
    purchase_price IS NULL;
    
    -- result
    product_name | purchase_price 
    --------------+----------------
     叉子         |               
     圆珠笔       |               
    (2 行记录)
    
    -- 查询不是空 NOT NULL
    SELECT
    product_name,
    purchase_price
    FROM
    Product
    WHERE
    purchase_price IS NOT NULL;
    
    -- result
    product_name | purchase_price 
    --------------+----------------
     T恤杉        |            500
     打孔器       |            320
     运动T恤      |           2800
     菜刀         |           2800
     高压锅       |           5000
     擦菜板       |            790
    (6 行记录)
    
    -- 逻辑运算 (AND)
    SELECT
    product_name,
    purchase_price
    FROM
    Product
    WHERE
    product_type = '厨房用具' AND sale_price >= 3000;
    
    -- result
    product_name | purchase_price 
    --------------+----------------
     菜刀         |           2800
     高压锅       |           5000
    (2 行记录)
    
    -- 用括号提高运算优先级
    SELECT
    product_name,
    product_type,
    regist_date
    FROM
    Product
    WHERE
    product_type = '办公用品'
    AND
    (regist_date = '2009-09-11' OR regist_date = '2009-09-20');
    
    -- result
    product_name | product_type | regist_date 
    --------------+--------------+-------------
     打孔器       | 办公用品     | 2009-09-11
    (1 行记录)
    
    -- count 函数
    -- count 计算行数 (只有此函数可以使用 * 号)
    SELECT
    count(*)
    FROM
    Product;
    
    -- result
    count 
    -------
         8
    (1 行记录)
    
    -- COUNT 计算行数 (排除 NUll)
    SELECT
    COUNT(purchase_price)
    FROM
    Product;
    
    -- result
    count 
    -------
         6
    (1 行记录)
    
    -- SUM 函数
    -- SUM 求和
    SELECT
    SUM(sale_price)
    FROM
    Product;
    
    -- result
    sum  
    -------
     16780
    (1 行记录)
    
    SELECT
    SUM(sale_price),
    SUM(purchase_price) -- 这里排除掉了两条 NULL 数据
    FROM
    Product;
    
    -- result
    sum  |  sum  
    -------+-------
     16780 | 12210
    (1 行记录)
    
    -- AVG 函数
    -- AVG 求平均值
    SELECT
    AVG(sale_price)
    FROM
    Product;
    
    -- result
    avg          
    -----------------------
     2097.5000000000000000
    (1 行记录)
    
    SELECT
    AVG(sale_price),
    AVG(purchase_price) -- 这里排除掉了两条 NULL 数据
    FROM
    Product;
    
    -- result
    avg          |          avg          
    -----------------------+-----------------------
     2097.5000000000000000 | 2035.0000000000000000
    (1 行记录)
    
    -- MAX 函数 (原则上, 可传入任何输入类型)
    -- MIN 函数 (原则上, 可传入任何输入类型)
    -- MAX 求最大值; MIN 求最小值
    SELECT
    MAX(sale_price),
    MIN(purchase_price)
    FROM
    Product;
    
    -- result
    max  | min 
    ------+-----
     6800 | 320
    (1 行记录)
    
    -- 1.去除重复数据 (去重); 2.计算商品有多少个类型
    SELECT
    COUNT(DISTINCT product_type)
    FROM
    Product;
    
    -- result
    count 
    -------
         3
    (1 行记录)
    
    -- SUM 函数 去重 与 不去重 的差异
    SELECT
    SUM(DISTINCT sale_price),
    SUM(sale_price)
    FROM
    Product;
    
    -- result
    sum  |  sum  
    -------+-------
     16280 | 16780
    (1 行记录)
    
    -- 分组
    -- 按照商品种类统计数据行数
    SELECT
    product_type,
    COUNT(*)
    FROM
    Product
    GROUP BY
    product_type;
    
    -- result
    product_type | count 
    --------------+-------
     衣服         |     2
     办公用品     |     2
     厨房用具     |     4
    (3 行记录)
    
    SELECT
    purchase_price,
    COUNT(*)  -- purchase_price 里有两条 NULL 数据
    FROM
    Product
    GROUP BY
    purchase_price;
    
    -- result
    purchase_price | count 
    ----------------+-------
                    |     2
                320 |     1
                500 |     1
               2800 |     2
               5000 |     1
                790 |     1
    (6 行记录)
    
    -- 执行顺序  FROM -> WHERE -> GROUP BY -> SELECT
    SELECT
    purchase_price,
    COUNT(*)
    FROM
    Product
    WHERE
    product_type = '衣服'
    GROUP BY
    purchase_price;
    
    -- result
    purchase_price | count 
    ----------------+-------
                500 |     1
               2800 |     1
    (2 行记录)
    
    -- 作为下面使用 HAVING 的对比
    SELECT
    product_type,
    COUNT(*)
    FROM
    Product
    GROUP BY
    product_type;
    
    -- result
    product_type | count 
    --------------+-------
     衣服         |     2
     办公用品     |     2
     厨房用具     |     4
    (3 行记录)
    
    -- WHERE 子句, 指定 行 所对应的条件 （具有 执行快、可创建索引 的性能优势）
    -- HAVING 子句, 对 分组(GROUP BY) 所对应的条件
    -- 执行顺序 FROM -> WHERE -> GROUP BY -> HAVING -> SELECT
    SELECT
    product_type,
    COUNT(*)
    FROM
    Product
    GROUP BY
    product_type
    HAVING
    COUNT(*) = 2;
    
    -- result
    product_type | count 
    --------------+-------
     衣服         |     2
     办公用品     |     2
    (2 行记录)
    
    -- 作为下面使用 HAVING 的对比
    SELECT
    product_type,
    AVG(sale_price)
    FROM
    Product
    GROUP BY
    product_type;
    
    -- result
    product_type |          avg          
    --------------+-----------------------
     衣服         | 2500.0000000000000000
     办公用品     |  300.0000000000000000
     厨房用具     | 2795.0000000000000000
    (3 行记录)
    
    -- (销售单价的平均值大于等于 2500)
    SELECT
    product_type,
    AVG(sale_price)
    FROM
    Product
    GROUP BY
    product_type
    HAVING
    AVG(sale_price) >= 2500;
    
    -- result
    product_type |          avg          
    --------------+-----------------------
     衣服         | 2500.0000000000000000
     厨房用具     | 2795.0000000000000000
    (2 行记录)
    
    
    
    

    -- 排序 ORDER BY
    -- 书写顺序 SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY
    -- 升序
    SELECT
    product_id,
    product_name,
    sale_price,
    purchase_price
    FROM
    Product
    ORDER BY
    sale_price; -- 省略了关键字 ASC
    
    -- result
    product_id | product_name | sale_price | purchase_price 
    ------------+--------------+------------+----------------
     0008       | 圆珠笔       |        100 |               
     0006       | 叉子         |        500 |               
     0002       | 打孔器       |        500 |            320
     0007       | 擦菜板       |        880 |            790
     0001       | T恤杉        |       1000 |            500
     0004       | 菜刀         |       3000 |           2800
     0003       | 运动T恤      |       4000 |           2800
     0005       | 高压锅       |       6800 |           5000
    (8 行记录)
    
    -- 降序
    SELECT
    product_id,
    product_name,
    sale_price,
    purchase_price
    FROM
    Product
    ORDER BY
    sale_price DESC;
    
    -- result
    product_id | product_name | sale_price | purchase_price 
    ------------+--------------+------------+----------------
     0005       | 高压锅       |       6800 |           5000
     0003       | 运动T恤      |       4000 |           2800
     0004       | 菜刀         |       3000 |           2800
     0001       | T恤杉        |       1000 |            500
     0007       | 擦菜板       |        880 |            790
     0002       | 打孔器       |        500 |            320
     0006       | 叉子         |        500 |               
     0008       | 圆珠笔       |        100 |               
    (8 行记录)
    
    -- 指定多个排序键 (按照销售单价和商品编号, 升序排序)
    SELECT
    product_id,
    product_name,
    sale_price
    FROM
    Product
    ORDER BY
    sale_price,
    product_id;
    
    -- result
    /* 先按 sale_price 升序, sale_price == 500
       有两个，然后按 product_id 升序
    /*
    product_id | product_name | sale_price 
    ------------+--------------+------------
     0008       | 圆珠笔       |        100
     0002       | 打孔器       |        500
     0006       | 叉子         |        500
     0007       | 擦菜板       |        880
     0001       | T恤杉        |       1000
     0004       | 菜刀         |       3000
     0003       | 运动T恤      |       4000
     0005       | 高压锅       |       6800
    
    -- ORDER BY 可以使用 别名
    SELECT
    product_id AS id,
    product_name,
    sale_price AS sp,
    purchase_price
    FROM
    Product
    ORDER BY
    sp,
    id;
    
    -- result
    id  | product_name |  sp  | purchase_price 
    ------+--------------+------+----------------
     0008 | 圆珠笔       |  100 |               
     0002 | 打孔器       |  500 |            320
     0006 | 叉子         |  500 |               
     0007 | 擦菜板       |  880 |            790
     0001 | T恤杉        | 1000 |            500
     0004 | 菜刀         | 3000 |           2800
     0003 | 运动T恤      | 4000 |           2800
     0005 | 高压锅       | 6800 |           5000
    (8 行记录)
    
    -- 使用 HAVING 和 ORDER BY 时的 执行顺序
    -- FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY
    
    -- 数据更新
    -- 创建表 ProductIns
    CREATE TABLE ProductIns
    (
      product_id CHAR(4) NOT NUll,
      product_name VARCHAR(100) NOT NULL,
      product_type VARCHAR(32) NOT NULL,
      sale_price INTEGER DEFAULT 0, -- 这里设置了默认值
      purchase_price INTEGER,
      regist_date DATE,
      PRIMARY KEY (product_name)
    );
    
    -- INSERT 插入
    INSERT INTO ProductIns
    (
      product_id,
      product_name,
      product_type,
      sale_price,
      purchase_price,
      regist_date
    ) -- 当按列的顺序插入全部列的数据时，这里是可以省略的。
    VALUES
    (
      '0001',
      'T恤杉',
      '衣服',
      1000,
      500,
      '2009-09-20'
    );
    
    -- result
    INSERT 0 1
    
    -- 多行插入 (不适用 Oracle)
    INSERT INTO ProductIns
    VALUES
    ('0002', '打孔器', '办公用品', 500, 320, '2009-09-11'),
    ('0003', '运动T恤', '衣服', 4800, 2800, NULL),
    ('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20');
    
    -- result
    INSERT 0 3
    
    -- 插入默认值 DEFAULT, 前提是 CREATE TABLE 是设置了默认值
    INSERT INTO ProductIns
    (
      product_id,
      product_name,
      product_type,
      sale_price,
      purchase_price,
      regist_date
    ) -- 当按列的顺序插入全部列的数据时，这里是可以省略的。
    VALUES
    (
      '0007',
      '擦菜板',
      '厨房用具',
      DEFAULT,
      790,
      '2009-04-28'
    );
    
    -- result
    INSERT 0 1
    
    -- 从其他表中复制数据
    -- 先创建一个 Product 表的复制
    CREATE TABLE ProductCopy
    (
      product_id CHAR(4) NOT NUll,
      product_name VARCHAR(100) NOT NULL,
      product_type VARCHAR(32) NOT NULL,
      sale_price INTEGER, 
      purchase_price INTEGER,
      regist_date DATE,
      PRIMARY KEY (product_name)
    );
    
    -- 将 Product 中的数据复制到 ProdcutCopy 中
    INSERT INTO ProductCopy
    (
      product_id,
      product_name,
      product_type,
      sale_price,
      purchase_price,
      regist_date
    )
    SELECT
      product_id,
      product_name,
      product_type,
      sale_price,
      purchase_price,
      regist_date
    FROM
     Product;
    
    -- result
    INSERT 0 8
    
    -- 上面的语句中的 SELECT 部分也可以使用 WHERE, GROUP BY 等子句 (ORDER BY 无效果)
    -- 首先创建一个 根据商品种类进行汇总 的表
    CREATE TABLE ProductType
    (
      product_type VARCHAR(32) NOT NULL,
      sum_sale_price INTEGER,
      sum_purchase_price INTEGER,
      PRIMARY KEY (product_type)
    );
    
    -- 从 Product 表中复制数据进行计算, 然后插入 ProductType
    INSERT INTO ProductType
      (product_type, sum_sale_price, sum_purchase_price)
    SELECT
      product_type, SUM(sale_price), SUM(purchase_price)
    FROM
      Product
    GROUP BY
      product_type;
    
    -- result
    INSERT 0 3
    
    -- 数据的删除
    -- 删除全部数据 DELETE 
    DELETE FROM Product;
    -- 删除全部数据 TRUNCATE (只能用来删除全部数据，性能比 DELETE 高)
    -- TRUNCATE 属于 RDBMS 自家实现的功能
    TRUNCATE Product;
    
    
    -- 条件删除 (删除只能使用 WHERE 子句)
    DELETE FROM
      Product
    WHERE
      sale_price >= 4000;
    
    -- result
    DELETE 2
    
    -- 数据的更新
    -- 将表中 regist_date 列全部更新为 2009-10-10
    UPDATE
      Product
    SET
      regist_date = '2009-10-10';
    
    -- result
    UPDATE 6
    
    -- 条件更新
    UPDATE
      Product
    SET
      sale_price = sale_price * 10
    WHERE
      product_type = '厨房用具';
    
    -- result
    UPDATE 3
    
    -- 更新 NULL 值
    UPDATE
      Product
    SET
      regist_date = NULL
    WHERE
      product_id = '0008';
    
    -- result
    UPDATE 1
    
    -- 多列更新
    UPDATE
      Product
    SET
      sale_price = sale_price / 10,
      purchase_price = purchase_price / 2
    WHERE
      product_type = '厨房用具';
    
    -- result
    UPDATE 3

    -- 事务
    -- RDBMS 对事务的实现有两种选择
    -- 1, 自动提交 (其实每条 sql 语句被自动的嵌入到了 事务 的语句中)
    -- 2, 直到用户手动 COMMIT 或者 ROLLBACK, 才算一个事物 (Orcale)
    
    /* 事务开始 的语句是由 RDBMS 自己实现的
       BEGIN TRANSACTION (SQL Server, PostgreSQL)
       START TRANSACTION (MySQL)
    */
    
    /* 事务结束 的语句只有
       COMMIT (提交) 和 ROLLBACK （回滚） 两种 (在 RDBMS 中通用)
    */
    
    BEGIN TRANSACTION;
    -- 将运动T恤的销售单价降低 1000
    UPDATE
      Product
    SET
      sale_price = sale_price - 1000
    WHERE
      product_name = '运动T恤';
    -- 将T恤杉的销售单价上浮 1000
    UPDATE
      Product
    SET
    	sale_price = sale_price + 1000
    WHERE
      product_name = 'T恤杉';
    COMMIT;
    
    -- 视图
    -- 1. 创建视图时 不能使用 ORDRE BY
    -- 2. 
    -- 创建视图
    CREATE VIEW ProductSum
    ( product_type, cnt_product )
    AS
    SELECT
      product_type, COUNT(*)
    FROM
      Product
    GROUP BY
      product_type;
    
    -- result
    CREATE VIEW
    
    -- 使用视图
    SELECT
      product_type, cnt_product
    FROM
      ProductSum;
    
    -- result
    product_type | cnt_product 
    --------------+-------------
     衣服         |           2
     办公用品     |           2
     厨房用具     |           4
    (3 行记录)
    
    -- 以视图创建视图 (多重视图) (尽量避免, 会降低性能)
    CREATE VIEW ProductSumJim
    ( product_type, cnt_product )
    AS
    SELECT
      product_type, cnt_product
    FROM
      ProductSum
    WHERE
      product_type = '办公用品';
    
    -- 删除视图
    DROP VIEW ProductSum;
    
    -- 删除关联视图
    DROP VIEW ProdcutSum CASCADE;
    
    -- 子查询 (不会像 视图 那样保存在存储介质当之, SELECT 在执行后就消失)
    SELECT
      product_type,
      cnt_product
    FROM
    (
      SELECT
        product_type,
        COUNT(*) AS cnt_product
      FROM
        Product
      GROUP BY
        product_type
    )
    AS
    ProductSum;
    
    -- result
    product_type | cnt_product 
    --------------+-------------
     衣服         |           2
     办公用品     |           2
     厨房用具     |           4
    (3 行记录)
    
    -- 标量子查询 (可在可以使用 常数 和 列名 的地方使用)
    
    -- 选出 销售单价 高于 平均单价 的商品
    SELECT
      product_id,
      product_name,
      sale_price
    FROM
      Product
    WHERE
      sale_price > (
        SELECT
          AVG(sale_price)
        FROM
          Product
    );
    
    -- result
    product_id | product_name | sale_price 
    ------------+--------------+------------
     0003       | 运动T恤      |       4000
     0004       | 菜刀         |       3000
     0005       | 高压锅       |       6800
    (3 行记录)
    
    SELECT
      product_id,
      product_name,
      sale_price,
      (
        SELECT
          AVG(sale_price)
        FROM
          Product
      ) AS avg_price
    FROM
      Product;
    
    -- result
    product_id | product_name | sale_price |       avg_price       
    ------------+--------------+------------+-----------------------
     0001       | T恤杉        |       1000 | 2097.5000000000000000
     0002       | 打孔器       |        500 | 2097.5000000000000000
     0003       | 运动T恤      |       4000 | 2097.5000000000000000
     0004       | 菜刀         |       3000 | 2097.5000000000000000
     0005       | 高压锅       |       6800 | 2097.5000000000000000
     0006       | 叉子         |        500 | 2097.5000000000000000
     0007       | 擦菜板       |        880 | 2097.5000000000000000
     0008       | 圆珠笔       |        100 | 2097.5000000000000000
    (8 行记录)
    
    SELECT
      product_type,
      AVG(sale_price)
    FROM
      Product
    GROUP BY
      product_type
    HAVING
      AVG(sale_price) > (
        SELECT
          AVG(sale_price)
        FROM
          Product
    );
    
    -- result
    product_type |          avg          
    --------------+-----------------------
     衣服         | 2500.0000000000000000
     厨房用具     | 2795.0000000000000000
    (2 行记录)
    
    -- 关联子查询
    -- 找出 同一类商品中 价格高于 这一类商品均价 的商品
    SELECT
      product_type,
      product_name,
      sale_price
    FROM
      Product
    AS
      P1
    WHERE
      sale_price > (
        SELECT
          AVG(sale_price)
        FROM
          Product
        AS
          P2
        WHERE
          P1.product_type = P2.product_type
        GROUP BY
          product_type
    );
    
    -- result
    product_type | product_name | sale_price 
    --------------+--------------+------------
     办公用品     | 打孔器       |        500
     衣服         | 运动T恤      |       4000
     厨房用具     | 菜刀         |       3000
     厨房用具     | 高压锅       |       6800
    (4 行记录)
## 一、实验目的
1.掌握系统中涉及的类的定义；  
2.应用顶层Object类中toString()方法；  
3.掌握static、final等修饰符的用法。  
## 二、实验内容
某学校给学生提供勤工俭学机会，选派部分学生参与实验室的卫生清洁工作。  
每个学生被分配若干间实验室，视实验室的卫生评分给予劳务费。  
例如：学生“张三”负责“计算机网络实验室”、“组成原理实验室”的清洁，每周被要检查，记录每间实验室的卫生评分。  
在某周的检查中，“计算机网络实验室”卫生得“优”，“组成原理实验室”卫生得“及格”。  
一次“优”按x元记录补助，一次“及格”按y元记录补助。  
（卫生标准分级、相应的等级补助标准，自行规定）按国家的税务制度，劳务费应按国家规定纳税，请统计一学期学生的实际收入。（国家最新工资纳税标准，请自行检索）。  
1.设计系统中的类（如学生、实验室等）；  
2.应用数组（或其他列表类）定义周数。方便赋值期间，一学期按5周计；  
3.每个学生负责的实验室数量不一定相同；  
4.对学期勤工俭学收入和纳税进行统计，求得实际收入；  
5.输出某学生的实验室清洁记录；  
6.国家最新纳税标准（系数），属于某一时期的特定固定值，与实例化对象没有关系，考虑应用static、final修饰。  
## 四、解题思路
1.定义Laboratory类和Student类。  
2.实例化学生和实验室。添加add_lab函数，将实验室分配给不同的同学。  
3.设置异常处理（try-catch），使评分控制在1-10之间。  
4.设置cal_money函数，通过学生打扫的实验室按照分数等级计算每周能获得的工资。  
5.设置一个税率类Tax  
6.设置税后收入函数cal_tax  

## 五、流程图 
![](https://github.com/audience11/the_fourth_work/blob/main/%E6%B5%81%E7%A8%8B%E5%9B%BE.png)
## 六、关键代码
1. 给学生分配实验室
```
stu1.add_lab(lab1);
stu1.add_lab(lab2);
stu2.add_lab(lab3);
stu3.add_lab(lab4);
```
2. 异常处理
```
try {
            Scanner in = new Scanner(System.in);
            System.out.println("请打分");
            for (int i = 0; i < 5; i++) {
                System.out.println("第" + (i + 1) + "周:");
                score[i] = in.nextInt();
                if(score[i]>0 & score[i]<=10){
                    continue;
                }
                else{
                    System.out.println("输入错误");
                    break;
                }
            }
        }
        catch (NumberFormatException e){
            System.out.println("数据结构异常");
        }
        catch (Exception e){
            System.out.println("异常");
        }
    }
    ```
3.计算全部所得钱数
'''
    public void cal_money(){
        int[] a = new int[18];

        for (int i = 0;i< labs.length;i++){
            if (labs[i] == null){
                continue;
            }
            else {
                double m = 0;
                System.out.println(labs[i].getName() + "收入统计：");
                a = labs[i].getScore(); //分数数组
                for(int j=0;j<18;j++){

                    if(a[j]>0 & a[j]<=5){ //5分一下及格
                        m = m + Laboratory.pass;
                    }
                    else if(a[j]>7 & a[j]<=10){ //7分以上优秀
                        m = m + Laboratory.great;
                    }
                    else if(a[j]>5 & a[j]<=7){  //其余良好
                        m = m + Laboratory.good;
                    }

                }
                System.out.println(m);
                money = m + money;
            }
        }
        System.out.println(this.name + "的总共收入" + money);
    }
    ```
4. 计算税收
   ```
   public void cal_tax(){
        if(money<=200){
            System.out.println(this.name + "的税后所得为"+ Math.round(money*(1- Tax.taxmin))+"\n");
        }
        else if(money>300 & money<=400){
            System.out.println(this.name + "的税后所得为"+ Math.round(money*(1- Tax.tax))+"\n");
        }
        else if(money>400){
            System.out.println(this.name + "的税后所得为"+ Math.round(money*(1- Tax.taxmax))+"\n");
        }
    }
    ```
## 七、运行截图
![](https://github.com/audience11/the_fourth_work/blob/main/%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.png)
## 八、实验感想
&emsp;&emsp;通过本次实验,我加深了对Java异常机制的理解,也应用了try catch结构做代码块异常判别。通过new一个数组,从而通过数组的下标取出内容，当下标不合法时就会出现数组下标越界异常。通过catch捕获异常,并对异常作出处理，同时练习了非访问控制修饰符static以及final的使用，学到了很多新知识，也感谢老师的辛勤付出。

```c#
using System;
using System.Collections.Generic;
using System.Diagnostics.Eventing.Reader;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApplication11
{
    // LINQ
    class Program
    {
        static void Main(string[] args)
        {
            //集合中查询值>8的数，并返回，多个条件的场合，var > 8 && xx == "aa"
            //orderby排序可多个字段，和sql类似
            var numList = from var in new List<int> { 3, 5, 8, 12, 50 } where var > 8 orderby var descending select var;

            foreach (int num in numList)
            {
                Console.WriteLine(num);
            }

            //扩展方法的写法(where里面是List里的每个变量对象，返回true的结果会返回)
            var numList2 = new List<int> { 3, 5, 8, 12, 50 }.Where(delegate(int num)
            {
                if (num > 8)
                {
                    return true;
                }
                else
                {
                    return false;
                }
            });
            foreach (int num in numList2)
            {
                Console.WriteLine(num);
            }

            //一般这样写（where里用Lambda表达式） ，多个条件的场合，var > 8 && xx == "aa"
            //orderby多条件的情况下，例：OrderBy(num=>num).ThenBy(num2=>num2);
            var numList3 = new List<int> { 3, 5, 8, 33, 12, 50 }.Where(num => num > 8).OrderByDescending(num=>num);
            foreach (int num in numList3)
            {
                Console.WriteLine(num);
            }




            //集合联合查询join on例(参照，不能实行)
            var res = from m in masterList
                join k in kongfuList on m.Kongfu equals k.Name
                where k.Power > 90
                select new { master = m, kongfu = k };

            foreach (String temp in res)
            {
                Console.WriteLine(temp);
            }



            //分组查询 into groups（把武林高手按照所学功夫分组，看一下哪个功夫修炼的人数最多）(参照，不能实行)
            var res2 = from k in konfuList
                join m in masterListList on k.Name equals m.Kongfu
                    into groups
                orderby groups.Count()
                select new { kongfu = k, count = groups.Count() };
            foreach (String temp in res)
            {
                Console.WriteLine(temp);
            }



            //按照自身字段分组group(参照，不能实行)
            var res = from m in masterList
                group m by m.Menpai
                into g
                select new { count = g.count(), key = g.Key };//g.Key Key表示按照那个属性分的组
            
            foreach (String temp in res)
            {
                Console.WriteLine(temp);
            }


            //量词操作符 any all 判断集合中是否满足某个条件(参照，不能实行)
            bool res = masterList.Any(m => m.Menpai == "丐帮");

            //bool res = masterList.All(m => m.Menpai == "丐帮"); //all意思是这个集合里所有元素都满足这个条件，才会返回true


            Console.ReadKey();
        }
    }
}
```
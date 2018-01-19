



```C# runnable
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

namespace LinqQueries
{
    class Program
    {
        static void Main(string[] args)
        {
            //string[] words = { "learning", "C#", "is", "fun" };
            //var query = (from word in words
            //                            where word.Length >= 2
            //                            select word).Skip(3);

            //foreach (var str in query)
            //    Console.WriteLine(str);



            //Console.ReadKey();

            List<Element> elements = BuildList();

            // LINQ Query.  
            var subset = from theElement in elements
                         let bigElement = theElement.Symbol.ToLower()
                         where bigElement == "ca"
                         select theElement;

            foreach (Element theElement in subset)
            {
                Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);
            }
            Console.ReadKey();

            // Output:  
            //  Calcium 20  
            //  Potassium 19  
            //  Scandium 21  

        }

        private static List<Element> BuildList()
        {
            return new List<Element>
    {
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
        }

        public class Element
        {
            public string Symbol { get; set; }
            public string Name { get; set; }
            public int AtomicNumber { get; set; }
        }
    }
}



```
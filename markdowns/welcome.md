# LINQ Examples


## Use of Let and Select
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

            List<Element> elements = BuildList();

            // LINQ Query.  
            var subset = from theElement in elements
                         let specificElement = theElement.Name.ToLower()
                         where specificElement.Contains("ca")
                         select theElement;

            foreach (Element theElement in subset)
            {
                Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);
            }
        }

        private static List<Element> BuildList()
        {
            return new List<Element>
    {
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}},
		{ new Element() { Symbol="V", Name="Vanadium", AtomicNumber=23}},
		{ new Element() { Symbol="Cr", Name="Chromium", AtomicNumber=24}}
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

## Use of orderby/groupBy
   
## Useful extension methods

### Cout()
### Skip()
### Any()

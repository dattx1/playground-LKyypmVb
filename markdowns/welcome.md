# LINQ Examples


## Use of Let and Select
```C# runnable
// { autofold
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
// }
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
// { autofold
        public class Element
        {
            public string Symbol { get; set; }
            public string Name { get; set; }
            public int AtomicNumber { get; set; }
        }
    }
}
// }
```

## Use of orderby/groupBy
```C# runnable
// { autofold
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
            // }
            List<Element> elements = BuildList();

            // LINQ Query.  
            var subset = from theElement in elements
                         group theElement by theElement.Family into familyGroup
                         orderby familyGroup.Key
                         select familyGroup;

            foreach (var familyGrp in subset)
            {
                Console.WriteLine("Family: {0}", familyGrp.Key);
                foreach (var element in familyGrp)
                {
                    Console.WriteLine("\t- {0}",element.Name);
                }
            }
        }

        private static List<Element> BuildList()
        {
            return new List<Element>
    {
        { new Element() { Family="Noble gas", Symbol="He", Name="Helium", AtomicNumber=2}},
        { new Element() { Family="Halogen", Symbol="F", Name="Fluorine", AtomicNumber=9}},
        { new Element() { Family="Noble gas", Symbol="Ne", Name="Neon", AtomicNumber=10}},
        { new Element() { Family="Halogen", Symbol="Cl", Name="Chlorine", AtomicNumber=17}},
        { new Element() { Family="Noble gas", Symbol="Ar", Name="Argon", AtomicNumber=18}},
        { new Element() { Family="Alkali metal", Symbol="Na", Name="Sodium", AtomicNumber=11}},
        { new Element() { Family="Noble gas", Symbol="Rn", Name="Radon", AtomicNumber=86}},
        { new Element() { Family="Alkali metal", Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Family="Halogen", Symbol="At", Name="Astatine", AtomicNumber=85}},
        { new Element() { Family="Alkali metal", Symbol="Li", Name="Lithium", AtomicNumber=3}}
    };
        }
        // { autofold
        public class Element
        {
            public string Symbol { get; set; }
            public string Name { get; set; }
            public int AtomicNumber { get; set; }
            public string Family { get; set; }
        }
    }
}
// }
```

   
## Useful extension methods

### Cout()
```C# runnable
// { autofold
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
            // }
            List<Element> elements = BuildList();

            // LINQ Query.  
            var subset = from theElement in elements
                         group theElement by theElement.Family into familyGroup
                         select new
                         {
                             Name = familyGroup.Key,
                             Count = familyGroup.Count()
                         };

            foreach (var familyGrp in subset)
            {
                Console.WriteLine("The {0} family has {1} members in the list.", familyGrp.Name, familyGrp.Count);
            }
        }

        private static List<Element> BuildList()
        {
            return new List<Element>
    {
        { new Element() { Family="Noble gas", Symbol="He", Name="Helium", AtomicNumber=2}},
        { new Element() { Family="Halogen", Symbol="F", Name="Fluorine", AtomicNumber=9}},
        { new Element() { Family="Noble gas", Symbol="Ne", Name="Neon", AtomicNumber=10}},
        { new Element() { Family="Halogen", Symbol="Cl", Name="Chlorine", AtomicNumber=17}},
        { new Element() { Family="Noble gas", Symbol="Ar", Name="Argon", AtomicNumber=18}},
        { new Element() { Family="Alkali metal", Symbol="Na", Name="Sodium", AtomicNumber=11}},
        { new Element() { Family="Noble gas", Symbol="Rn", Name="Radon", AtomicNumber=86}},
        { new Element() { Family="Alkali metal", Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Family="Halogen", Symbol="At", Name="Astatine", AtomicNumber=85}},
        { new Element() { Family="Alkali metal", Symbol="Li", Name="Lithium", AtomicNumber=3}}
    };
        }
        // { autofold
        public class Element
        {
            public string Symbol { get; set; }
            public string Name { get; set; }
            public int AtomicNumber { get; set; }
            public string Family { get; set; }
        }
    }
}
// }
```
### Skip()
```C# runnable
// { autofold
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
            // }
            List<Element> elements = BuildList();

            // LINQ Query.  
            var subset = (from theElement in elements
                         orderby theElement.Name
                         select theElement).Skip(7);

            foreach (var element in subset)
            {
                Console.WriteLine(element.Name);
            }
        }

        private static List<Element> BuildList()
        {
            return new List<Element>
    {
        { new Element() { Family="Noble gas", Symbol="He", Name="Helium", AtomicNumber=2}},
        { new Element() { Family="Halogen", Symbol="F", Name="Fluorine", AtomicNumber=9}},
        { new Element() { Family="Noble gas", Symbol="Ne", Name="Neon", AtomicNumber=10}},
        { new Element() { Family="Halogen", Symbol="Cl", Name="Chlorine", AtomicNumber=17}},
        { new Element() { Family="Noble gas", Symbol="Ar", Name="Argon", AtomicNumber=18}},
        { new Element() { Family="Alkali metal", Symbol="Na", Name="Sodium", AtomicNumber=11}},
        { new Element() { Family="Noble gas", Symbol="Rn", Name="Radon", AtomicNumber=86}},
        { new Element() { Family="Alkali metal", Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Family="Halogen", Symbol="At", Name="Astatine", AtomicNumber=85}},
        { new Element() { Family="Alkali metal", Symbol="Li", Name="Lithium", AtomicNumber=3}}
    };
        }
        // { autofold
        public class Element
        {
            public string Symbol { get; set; }
            public string Name { get; set; }
            public int AtomicNumber { get; set; }
            public string Family { get; set; }
        }
    }
}
// }
```
### Join
```C# runnable
// { autofold
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
		            // }
            List<Element> elementsNames = BuildList();
            List<SymbolElement> elementsSymbols = BuildListSymbols();

            // LINQ Query.  
            var subset = from theElement in elementsNames
                         join sym in elementsSymbols on theElement.AtomicNumber equals sym.AtomicNumber
                         where theElement.AtomicNumber == 17
                         select new {ElementSymbol = sym.Symbol, ElementName =theElement.Name};

            foreach (var element in subset)
            {
                Console.WriteLine("The {0} element symbol is : {1}",element.ElementName,element.ElementSymbol);
            }
            Console.ReadKey();
        }

        private static List<Element> BuildList()
        {
            return new List<Element>
    {
        { new Element() { Name="Helium", AtomicNumber=2}},
        { new Element() { Name="Fluorine", AtomicNumber=9}},
        { new Element() { Name="Neon", AtomicNumber=10}},
        { new Element() { Name="Chlorine", AtomicNumber=17}},
        { new Element() { Name="Argon", AtomicNumber=18}},
        { new Element() { Name="Sodium", AtomicNumber=11}},
        { new Element() { Name="Radon", AtomicNumber=86}},
        { new Element() { Name="Potassium", AtomicNumber=19}},
        { new Element() { Name="Astatine", AtomicNumber=85}},
        { new Element() { Name="Lithium", AtomicNumber=3}}
    };
        }

        private static List<SymbolElement> BuildListSymbols()
        {
            return new List<SymbolElement>
    {
        { new SymbolElement() { Symbol="He", AtomicNumber=2}},
        { new SymbolElement() { Symbol="F", AtomicNumber=9}},
        { new SymbolElement() { Symbol="Ne", AtomicNumber=10}},
        { new SymbolElement() { Symbol="Cl", AtomicNumber=17}},
        { new SymbolElement() { Symbol="Ar", AtomicNumber=18}},
        { new SymbolElement() { Symbol="Na", AtomicNumber=11}},
        { new SymbolElement() { Symbol="Rn", AtomicNumber=86}},
        { new SymbolElement() { Symbol="K", AtomicNumber=19}},
        { new SymbolElement() { Symbol="At", AtomicNumber=85}},
        { new SymbolElement() { Symbol="Li", AtomicNumber=3}}
    };
        }
		// { autofold
        public class Element
        {
            public string Name { get; set; }
            public int AtomicNumber { get; set; }
            public string Family { get; set; }
        }
        public class SymbolElement
        {
            public string Symbol { get; set; }
            public int AtomicNumber { get; set; }
            public string Family { get; set; }
        }
    }
}
// }
```



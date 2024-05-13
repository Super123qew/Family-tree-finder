# Family-tree-finder (Justin, Karl, Cristian) if its not done by the time you look I tried my best

FYI If a lot of the code seems similar it is because it is very parallel to Danes group they helped me (Justin) a lot in figuring out the algorithm for the problem

 - Contains the source code and documentation
- [Family tree, same as rubric](https://www.familyecho.com/?p=D7GMC&c=ybfar0kdyj&f=796759587492087536)
- [Primary Code](https://openprocessing.org/sketch/2261725)
 
Problem:

-Give any two members in a family tree, and display their relationship.
 
## Input:

-Family tree


## ADDITIONAL:
- [ ] Generate both masculine and feminine terms for family member relations (masculine/neutral  is going to be the default term) [x]
- [ ] Implement a more efficient search method
- [x] ~~**remove the chance of the 2 people chosen twice being the same person**~~

## Solution:

Utilize the family tree and the idea of consanguinity to find the relationship between the two randomly selected people in a tree. It will search through the generation, and search for a common ancestor to determine if they are in the same family line. If not, trace their ancestry  to determine other family relationships (uncles, grandparents, aunt, etc.)


## Steps/Algorithm:
-**TLDR: Uses generations to compare and find the relationship**

* Generate the family tree 
* Randomly pick 2 people from the tree
* Determine what generation each person belongs to (In comparison to the Origin person)
* If in the same gen, proceed to check for sibling relationship (same parents?)
* If not, identify the individual from the lowest gen and start tracing lineage upwards
* Trace the lineage of both individuals through their respective parents, grandparents, etc
* Keep track of the number of generations jumped for both until a common ancestor is found
* Utilizing the number of generations jumped by either, determines the relation based on the consanguinity chart. Utilize the chart to establish what the relationship is between the two
* Print the result


## PseudoCode


1. Create a class of people with their name, generation, and who their parents are.
2. Create an array of items containing relationships in order from the consanguinity scale.
3. Randomly choose two people within the family tree for comparison using the random[family] function. 
4. Calculate a method to find the original member of the tree then determine if they are sibling, parent, niece or nephew, etc. using a for loop
   - Implement a check to identify if the 1st or 2nd person is the original person (and let the origin of both equal false unless either person is the original member of the tree)
   - Implement a counter to store the value of each jump from each person to the closest common ancestor (Base value=0)
   -
5. Utilize an array that contains the consanguinity chart to determine the relationship between the people using the beforehand counted values
6. Calculate the generational jumps between the two individuals





## Runtime Efficiency/complexity:



## Trades-offs


## Source Code: (Last updated May 12)

```js

class Person {
		constructor (name,gen, parent = null) {
		this.name = name
		this.gen = gen
		this.parent = parent
	
		}
}

let elizabeth = new Person('Elizabeth', 1, "nobody");
let rosanne = new Person('Rosanne', 2, elizabeth);
let ruthanne = new Person('Ruthanne', 2, elizabeth);
let donnie = new Person('Donnie', 2, elizabeth);
let patricia = new Person('Patricia', 2, elizabeth);
let marj = new Person('Marj', 2, elizabeth);
let kim = new Person('Kim', 3, marj);
let monica = new Person('Monica', 3, marj);
let martin = new Person('Martin', 3, marj);
let gabe = new Person('Gabe', 3, marj);
let john = new Person('John', 3, marj);
let ben = new Person('Ben', 3, marj);
let jerome = new Person('Jerome', 3, marj);
let john_G = new Person('John G', 4, kim);
let jamie = new Person('Jamie', 4, kim);
let julia = new Person('Julia', 4, kim);
let phil = new Person('Phil', 4, monica);
let alley = new Person('Alley', 4, monica);
let anna = new Person('Anna', 4, monica);
let steven = new Person('Steven', 4, monica);
let ellane = new Person('Ellane', 4, gabe);
let jake = new Person('Jake', 4, gabe);
let veera = new Person('Veera', 4, jerome);
let precila = new Person('Precila', 4, jerome);
let clarence = new Person('Clarence', 4, jerome);
let lincoln = new Person('Lincoln', 5, phil);
let mo = new Person('Mo', 5, ellane);

let family = [elizabeth, rosanne, ruthanne, donnie, patricia, marj, kim, monica, martin, gabe, john, ben, jerome, john_G, jamie, julia, phil, alley, anna, steven, ellane, jake, veera, precila, clarence, lincoln, mo];



let consanguinityChart = [
               ['Self', 'Children', 'Grandchildren', 'Great-grandchildren'],
    ['Parent', 'Sibling', 'Nephew/Niece', 'Great nephew/niece', 'Great-grand nephew/niece'],
    ['Grandparent', 'Uncle/Aunt', 'First cousin', 'First cousin once removed', 'First cousin twice removed', 'First cousin thrice removed'],
    ['Great grandparent', 'Great uncle/aunt', 'First cousin once removed', 'Second cousin', 'Second cousin once removed', 'Second cousin twice removed', 'Second cousin thrice removed'],
    ['Great-great grandparent', 'Great-grand uncle/aunt', 'First cousin twice removed', 'Second cousin once removed', 'Third cousin', 'Third cousin once removed', 'Third cousin twice removed', 'Third cousin thrice removed']
];



function setup() {
    createCanvas(windowWidth, windowHeight);

	let person1, person2
	
	do {
		person1= random(family)
		person2=random(family)
	} while (person1 === person2)
    

    print('People chosen are ' + person1.name + ' and ' + person2.name);
    let relation = relationCheck(person1, person2, family); // Call relationCheck function
    print(person1.name + ' is the ' + consanguinityChart[countPerson2][countPerson1] +   ' to ' + person2.name); // Print out the result

}

let origin1 = true
let origin2 = true
let countPerson1 = 0
let countPerson2 =0

function relationCheck (person1,person2, family) {
	
	
	
	for (i=0; i < family.length -1 ; i++) {
		//check if person1 is the origin member
		if (person1.parent === 'origin') {
			origin1= false
			
		
		}
		if (person2.parent === 'origin') {
		 origin2 = false
		
		}
		//break loop if names match
		if (person1.name === person2.name ) {
			break;
			
		}
		//Move up person1 parent hierachy
		if (person1.gen >= person2.gen && origin1) {
			if (origin1) {
			countPerson1++
			person1 = person1.parent
		}
		}
		//move up person2's parent hierachy
		if (person2 <= person1.gen && origin2) {
			if (origin2) {
 			countPerson2++
			person2 = person2.parent
			}
		}
		
		
	} 
}
```





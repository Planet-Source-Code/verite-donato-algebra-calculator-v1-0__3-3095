<div align="center">

## Algebra Calculator V1\.0


</div>

### Description

This C++ application runs under Windows via the MS-DOS prompt. It will compute the value of the unknown for a simple algebraic equation such as 3x+5=10. It has limited functionality, and cannot combine like terms or interpret mathematical operations more complex than +, -, *, /. For college or high-school math students, though, it can be useful. As long as you constrain yourself to the aforementioned guidelines, you'll be fine.
 
### More Info
 
This application is relatively simplistic; it cannot combine like terms, and it cannot handle any operation other than the standard "+, -, *, /, =". I will distribute a V2.0 in a few years, after I take some more mathematics courses.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Verite Donato](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/verite-donato.md)
**Level**          |Advanced
**User Rating**    |4.1 (33 globes from 8 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, UNIX C\+\+
**Category**       |[Math](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/math__3-12.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/verite-donato-algebra-calculator-v1-0__3-3095/archive/master.zip)





### Source Code

```
#include <iostream.h>
#include <string.h>
#include <math.h>
#include <ctype.h>
#include <stdlib.h>
double parseEquation ( char * );
struct term {
  double num;
  int hasUnknown;
  char oper;
  int negate;
};
struct equation {
  struct term t[10];
};
int main () {
  char equation [ 256 ];
  char ch;
  double solution;
  cout << "Algebra Calculator\n";
  cout << "Written by Verite Donato\n\n";
  cout << "Please enter an equation: ";
  cin.getline ( equation, sizeof(equation) );
  cout << "Solving equation: " << equation << " . . .\n";
  solution = parseEquation ( equation );
  	cout << "The solution to " << equation << " is: " << solution << ".\n\n";
	cout << "Thank you for using the Algebra Calculator!\n";
	cout << "Have a great day!\n\n";
  return 0;
}
double parseEquation ( char *eq ) {
  struct equation eqStruct;
  int unsigned i = 0, j = 0, numTerms = 0, k = 0, u = 0, flag = 0;
  double lastTerm = 0, unknownTerm = 0;
  char *tmp;
  tmp = (char *) malloc ( 256 );
  for ( i = 0; i < strlen(eq); ) {
	k = 0;
	if ( i > 0 )
	  eqStruct.t[j].oper = eq[i++];
	else {
	  if ( isdigit(eq[i]) || isalpha(eq[i]) )
		eqStruct.t[j].oper = '+';
	  else {
		eqStruct.t[j].oper = eq[i++];
	  }
	}
    if ( eq[i] == '-' ) {
   	  eqStruct.t[j].negate = 1;
   	  i++;
    }
    else
   	  eqStruct.t[j].negate = 0;
	if ( isdigit(eq[i]) ) {
 	  while ( isdigit(eq[i]) ) {
	    tmp[k++] = eq[i++];
      }
      tmp[k] = '\0';
 	  eqStruct.t[j].num = strtod (tmp, NULL);
	}
	else {
	  eqStruct.t[j].num = 1;
	}
	if ( eqStruct.t[j].negate )
		eqStruct.t[j].num -= eqStruct.t[j].num * 2;
	if ( isalpha(eq[i]) ) {
	  eqStruct.t[j].hasUnknown = 1;
	  i++;
	}
    else {
	  eqStruct.t[j].hasUnknown = 0;
	}
	j++;
  }
  numTerms = j;
  for ( j = 0; j < numTerms; j++ ) {
    if ( eqStruct.t[j].oper == '=' ) {
	  lastTerm = eqStruct.t[j].num;
	  flag = 1;
 	  continue;
	}
	if ( flag == 1 ) {
	  cout << lastTerm << eqStruct.t[j].oper << eqStruct.t[j].num << "\n";
 	  switch ( eqStruct.t[j].oper ) {
  		case '+':
	    lastTerm += eqStruct.t[j].num;
  	    break;
 	    case '-':
   		lastTerm -= eqStruct.t[j].num;
		break;
	    case '*':
	    lastTerm *= eqStruct.t[j].num;
  		break;
	    case '/':
 		lastTerm /= eqStruct.t[j].num;
	    break;
  		default:
	    cout << "Invalid operation: " << eqStruct.t[j].oper << "\n\n";
 	    exit ( 1 );
	  }
	}
  }
  for ( j = 0; j < numTerms; j++ ) {
	if ( eqStruct.t[j].hasUnknown ) {
	  unknownTerm = eqStruct.t[j].num;
	  u = j;
	  continue;
	}
	if ( eqStruct.t[j].oper == '=' )
	  break;
	switch ( eqStruct.t[j].oper ) {
	  case '+':
	    lastTerm -= eqStruct.t[j].num;
	    break;
	  case '-':
	    lastTerm += eqStruct.t[j].num;
	    break;
	  case '*':
	    lastTerm /= eqStruct.t[j].num;
	    break;
	  case '/':
	    lastTerm *= eqStruct.t[j].num;
	    break;
	  default:
	    cout << "Invalid operation: " << eqStruct.t[j].oper << "\n\n";
   	    exit ( 1 );
    }
  }
  if ( unknownTerm != 0 ) {
	if ( eqStruct.t[u].oper == '-' )
	  unknownTerm -= unknownTerm * 2;
    lastTerm = lastTerm / unknownTerm;
  }
  else {
    cout << "Error: Division by zero! Returning 0 . . .\n\n";
    return 0;
  }
  return lastTerm;
}
```


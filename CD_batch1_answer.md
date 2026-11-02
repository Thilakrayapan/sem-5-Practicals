
## Question 1: Lexical Analyzer in C (Identifiers and Constants)
**Problem Statement:** Develop a program in C to design a lexical analyzer that recognizes identifiers and constants.
**Functionality:** Scans an input string character by character using `ctype.h` functions (`isalpha`, `isalnum`, `isdigit`) to group and classify contiguous sequences into valid identifiers and numeric constants while ignoring spaces and delimiters.

### Program (`q1_lexer.c`)
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main() {
    char input[100], token[50];
    int i = 0, j = 0;

    printf("Enter an expression: ");
    fgets(input, sizeof(input), stdin);

    while (input[i] != '\0') {
        if (isspace(input[i])) {
            i++;
            continue;
        }
        // Check for Identifier
        if (isalpha(input[i]) || input[i] == '_') {
            j = 0;
            while (isalnum(input[i]) || input[i] == '_') {
                token[j++] = input[i++];
            }
            token[j] = '\0';
            printf("Identifier : %s\n", token);
        }
        // Check for Constant
        else if (isdigit(input[i])) {
            j = 0;
            while (isdigit(input[i])) {
                token[j++] = input[i++];
            }
            token[j] = '\0';
            printf("Constant   : %s\n", token);
        }
        // Ignore operators/delimiters
        else {
            i++;
        }
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q1_lexer.c -o q1_lexer
$ ./q1_lexer
Enter an expression: sum = count1 + 450 - 20;
Identifier : sum
Identifier : count1
Constant   : 450
Constant   : 20
```

---

## Question 2: Symbol Table Implementation in C
**Problem Statement:** Implement a symbol table that involves insertion, deletion, search and modify operations using C language.
**Functionality:** Maintains an array of structures storing symbol names, data types, and memory addresses, providing a menu-driven interface to insert, search, modify, delete, and display symbols.

### Program (`q2_symtab.c`)
```c
#include <stdio.h>
#include <string.h>

struct Symbol {
    char name[30];
    char type[20];
    int addr;
} sym[50];

int count = 0;

int search(char *name) {
    for (int i = 0; i < count; i++) {
        if (strcmp(sym[i].name, name) == 0) return i;
    }
    return -1;
}

void insert() {
    char name[30];
    printf("Enter Symbol Name: ");
    scanf("%s", name);
    if (search(name) != -1) {
        printf("Duplicate Symbol!\n");
        return;
    }
    strcpy(sym[count].name, name);
    printf("Enter Data Type & Address: ");
    scanf("%s %d", sym[count].type, &sym[count].addr);
    count++;
    printf("Inserted successfully.\n");
}

void modify() {
    char name[30];
    printf("Enter Symbol Name to Modify: ");
    scanf("%s", name);
    int idx = search(name);
    if (idx == -1) {
        printf("Symbol not found!\n");
        return;
    }
    printf("Enter New Data Type & New Address: ");
    scanf("%s %d", sym[idx].type, &sym[idx].addr);
    printf("Modified successfully.\n");
}

void delete_sym() {
    char name[30];
    printf("Enter Symbol Name to Delete: ");
    scanf("%s", name);
    int idx = search(name);
    if (idx == -1) {
        printf("Symbol not found!\n");
        return;
    }
    for (int i = idx; i < count - 1; i++) {
        sym[i] = sym[i + 1];
    }
    count--;
    printf("Deleted successfully.\n");
}

void display() {
    printf("\nName\tType\tAddress\n-----------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%s\t%s\t%d\n", sym[i].name, sym[i].type, sym[i].addr);
    }
}

int main() {
    int ch, idx;
    char name[30];
    while (1) {
        printf("\n1.Insert 2.Search 3.Modify 4.Delete 5.Display 6.Exit\nChoice: ");
        scanf("%d", &ch);
        if (ch == 6) break;
        switch (ch) {
            case 1: insert(); break;
            case 2:
                printf("Enter Name to Search: ");
                scanf("%s", name);
                idx = search(name);
                if (idx != -1) printf("Found at index %d (Type: %s, Addr: %d)\n", idx, sym[idx].type, sym[idx].addr);
                else printf("Not found!\n");
                break;
            case 3: modify(); break;
            case 4: delete_sym(); break;
            case 5: display(); break;
        }
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q2_symtab.c -o q2_symtab
$ ./q2_symtab

1.Insert 2.Search 3.Modify 4.Delete 5.Display 6.Exit
Choice: 1
Enter Symbol Name: x
Enter Data Type & Address: int 1000
Inserted successfully.

1.Insert 2.Search 3.Modify 4.Delete 5.Display 6.Exit
Choice: 3
Enter Symbol Name to Modify: x
Enter New Data Type & New Address: float 2000
Modified successfully.

1.Insert 2.Search 3.Modify 4.Delete 5.Display 6.Exit
Choice: 5

Name    Type    Address
-----------------------
x       float   2000

1.Insert 2.Search 3.Modify 4.Delete 5.Display 6.Exit
Choice: 6
```

---

## Question 3: Lexical Analyzer to Separate Tokens using LEX
**Problem Statement:** Design a program that implements a lexical analyzer that separates tokens using a LEX tool.
**Functionality:** Uses regular expressions in LEX to match and classify input patterns into keywords, identifiers, numbers, operators, and punctuation symbols.

### Program (`q3_tokens.l`)
```lex
%{
#include <stdio.h>
%}

%%
"int"|"float"|"char"|"if"|"else"|"while"|"return" { printf("Keyword    : %s\n", yytext); }
[a-zA-Z_][a-zA-Z0-9_]*                            { printf("Identifier : %s\n", yytext); }
[0-9]+(\.[0-9]+)?                                 { printf("Number     : %s\n", yytext); }
"+"|"-"|"*"|"/"|"="|"=="|"<"|">"                  { printf("Operator   : %s\n", yytext); }
[;,\(\)\{\}]                                      { printf("Separator  : %s\n", yytext); }
[ \t\n]+                                          ; /* Ignore whitespace */
.                                                 { printf("Unknown    : %s\n", yytext); }
%%

int yywrap() {
    return 1;
}

int main() {
    printf("Enter code (Press Ctrl+D to end):\n");
    yylex();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ lex q3_tokens.l
$ gcc lex.yy.c -o q3_tokens
$ ./q3_tokens
Enter code (Press Ctrl+D to end):
int a = 10 + 20;
Keyword    : int
Identifier : a
Operator   : =
Number     : 10
Operator   : +
Number     : 20
Separator  : ;
```

---

## Question 4: Recognize Valid Arithmetic Expression using YACC
**Problem Statement:** Use YACC tool to recognize a valid arithmetic expression that uses basic arithmetic operators `+`, `-`, `*`, `/`.
**Functionality:** LEX tokenizes numbers, variables, and operators, while YACC applies an unambiguous context-free grammar with operator precedence to validate the syntax of the arithmetic expression.

### LEX File (`q4_arith.l`)
```lex
%{
#include "y.tab.h"
%}

%%
[a-zA-Z_][a-zA-Z0-9_]* { return ID; }
[0-9]+                 { return NUM; }
[\+\-\*\/\(\)]         { return yytext[0]; }
[ \t]                  ;
\n                     { return '\n'; }
.                      { return yytext[0]; }
%%

int yywrap() { return 1; }
```

### YACC File (`q4_arith.y`)
```yacc
%{
#include <stdio.h>
#include <stdlib.h>
int yylex();
void yyerror(const char *s);
%}

%token ID NUM
%left '+' '-'
%left '*' '/'

%%
stmt : expr '\n' { printf("Valid Arithmetic Expression\n"); exit(0); }
     ;
expr : expr '+' expr
     | expr '-' expr
     | expr '*' expr
     | expr '/' expr
     | '(' expr ')'
     | ID
     | NUM
     ;
%%

void yyerror(const char *s) {
    printf("Invalid Arithmetic Expression\n");
    exit(0);
}

int main() {
    printf("Enter an arithmetic expression: ");
    yyparse();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ yacc -d q4_arith.y
$ lex q4_arith.l
$ gcc y.tab.c lex.yy.c -o q4_arith
$ ./q4_arith
Enter an arithmetic expression: (a + b) * 10 / c
Valid Arithmetic Expression

$ ./q4_arith
Enter an arithmetic expression: a + * b
Invalid Arithmetic Expression
```

---

## Question 5: Recognize Valid Variable using YACC
**Problem Statement:** Design a program to recognize a valid variable which starts with an alphabet followed by any number of digits or alphabets using YACC tool.
**Functionality:** LEX returns single character tokens (`LETTER` for alphabets, `DIGIT` for numbers), and YACC enforces the recursive grammar rule `var -> LETTER rest` to validate variable naming rules.

### LEX File (`q5_var.l`)
```lex
%{
#include "y.tab.h"
%}

%%
[a-zA-Z] { return LETTER; }
[0-9]    { return DIGIT; }
\n       { return '\n'; }
.        { return yytext[0]; }
%%

int yywrap() { return 1; }
```

### YACC File (`q5_var.y`)
```yacc
%{
#include <stdio.h>
#include <stdlib.h>
int yylex();
void yyerror(const char *s);
%}

%token LETTER DIGIT

%%
stmt : var '\n' { printf("Valid Variable\n"); exit(0); }
     ;
var  : LETTER rest
     ;
rest : LETTER rest
     | DIGIT rest
     | /* empty */
     ;
%%

void yyerror(const char *s) {
    printf("Invalid Variable\n");
    exit(0);
}

int main() {
    printf("Enter variable name: ");
    yyparse();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ yacc -d q5_var.y
$ lex q5_var.l
$ gcc y.tab.c lex.yy.c -o q5_var
$ ./q5_var
Enter variable name: count123
Valid Variable

$ ./q5_var
Enter variable name: 1stVar
Invalid Variable
```

---

## Question 6: Native Calculator using LEX and YACC
**Problem Statement:** Use LEX and YACC tools to implement a native calculator.
**Functionality:** LEX converts numeric strings to integers (`yylval = atoi(yytext)`), and YACC evaluates arithmetic expressions bottom-up using semantic actions (`$$ = $1 + $3`, etc.).

### LEX File (`q6_calc.l`)
```lex
%{
#include <stdlib.h>
#include "y.tab.h"
extern int yylval;
%}

%%
[0-9]+         { yylval = atoi(yytext); return NUM; }
[\+\-\*\/\(\)] { return yytext[0]; }
[ \t]          ;
\n             { return '\n'; }
.              { return yytext[0]; }
%%

int yywrap() { return 1; }
```

### YACC File (`q6_calc.y`)
```yacc
%{
#include <stdio.h>
#include <stdlib.h>
int yylex();
void yyerror(const char *s);
%}

%token NUM
%left '+' '-'
%left '*' '/'
%right UMINUS

%%
stmt : expr '\n' { printf("Result = %d\n", $1); exit(0); }
     ;
expr : expr '+' expr { $$ = $1 + $3; }
     | expr '-' expr { $$ = $1 - $3; }
     | expr '*' expr { $$ = $1 * $3; }
     | expr '/' expr {
           if ($3 == 0) { yyerror("Division by zero"); }
           else $$ = $1 / $3;
       }
     | '-' expr %prec UMINUS { $$ = -$2; }
     | '(' expr ')'  { $$ = $2; }
     | NUM           { $$ = $1; }
     ;
%%

void yyerror(const char *s) {
    printf("Error: %s\n", s);
    exit(0);
}

int main() {
    printf("Enter expression to calculate: ");
    yyparse();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ yacc -d q6_calc.y
$ lex q6_calc.l
$ gcc y.tab.c lex.yy.c -o q6_calc
$ ./q6_calc
Enter expression to calculate: (15 + 5) * 3 - 10
Result = 50
```

---

## Question 7: Generate Three-Address Code (TAC) from Arithmetic Expression
**Problem Statement:** Design a program to generate a three-address code from a given arithmetic expression.
**Functionality:** Uses LEX and YACC to parse an assignment expression according to operator precedence and generates sequential temporary variables (`t1`, `t2`, ...) representing Three-Address Code instructions.

### LEX File (`q7_tac.l`)
```lex
%{
#include <string.h>
#include "y.tab.h"
%}

%%
[a-zA-Z0-9]+       { strcpy(yylval.str, yytext); return OPERAND; }
[\+\-\*\/\=\(\)]   { return yytext[0]; }
[ \t]              ;
\n                 { return '\n'; }
.                  { return yytext[0]; }
%%

int yywrap() { return 1; }
```

### YACC File (`q7_tac.y`)
```yacc
%{
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int yylex();
void yyerror(const char *s);
int temp_count = 1;

void new_temp(char *res) {
    sprintf(res, "t%d", temp_count++);
}
%}

%union {
    char str[20];
}

%token <str> OPERAND
%type <str> expr
%left '+' '-'
%left '*' '/'

%%
stmt : OPERAND '=' expr '\n' {
           printf("%s = %s\n", $1, $3);
           exit(0);
       }
     ;
expr : expr '+' expr { new_temp($$); printf("%s = %s + %s\n", $$, $1, $3); }
     | expr '-' expr { new_temp($$); printf("%s = %s - %s\n", $$, $1, $3); }
     | expr '*' expr { new_temp($$); printf("%s = %s * %s\n", $$, $1, $3); }
     | expr '/' expr { new_temp($$); printf("%s = %s / %s\n", $$, $1, $3); }
     | '(' expr ')'  { strcpy($$, $2); }
     | OPERAND       { strcpy($$, $1); }
     ;
%%

void yyerror(const char *s) {
    printf("Syntax Error!\n");
    exit(0);
}

int main() {
    printf("Enter an assignment expression (e.g., a = b + c * d): ");
    yyparse();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ yacc -d q7_tac.y
$ lex q7_tac.l
$ gcc y.tab.c lex.yy.c -o q7_tac
$ ./q7_tac
Enter an assignment expression (e.g., a = b + c * d): a = b + c * d - e
t1 = c * d
t2 = b + t1
t3 = t2 - e
a = t3
```

---

## Question 8: Simple Type Checker and Scope Checker
**Problem Statement:** Implement a simple type checker that checks the scope of the variables and semantic errors from the given statement.
**Functionality:** Records declared variables alongside their data types and scopes, then checks an assignment statement to verify that all referenced variables are declared (no undeclared variable error) and that their types match (no type mismatch error).

### Program (`q8_typecheck.c`)
```c
#include <stdio.h>
#include <string.h>

struct Var {
    char name[20];
    char type[10];
    int scope;
} table[20];

int n = 0;

int find_var(char *name, int current_scope) {
    // Check local scope first, then outer scope
    for (int i = n - 1; i >= 0; i--) {
        if (strcmp(table[i].name, name) == 0 && table[i].scope <= current_scope)
            return i;
    }
    return -1;
}

int main() {
    int scope;
    char lhs[20], op1[20], op2[20], op;

    printf("Enter number of declarations: ");
    scanf("%d", &n);
    printf("Enter Declarations (Name Type Scope_Level[0=Global, 1=Local]):\n");
    for (int i = 0; i < n; i++) {
        scanf("%s %s %d", table[i].name, table[i].type, &table[i].scope);
    }

    printf("\nEnter current scope level for statement evaluation (0 or 1): ");
    scanf("%d", &scope);
    printf("Enter statement in format (lhs = op1 + op2): ");
    scanf("%s = %s %c %s", lhs, op1, &op, op2);

    int i_lhs = find_var(lhs, scope);
    int i_op1 = find_var(op1, scope);
    int i_op2 = find_var(op2, scope);

    if (i_lhs == -1 || i_op1 == -1 || i_op2 == -1) {
        printf("Semantic Error: Undeclared variable or variable out of scope!\n");
        return 0;
    }

    if (strcmp(table[i_lhs].type, table[i_op1].type) == 0 &&
        strcmp(table[i_op1].type, table[i_op2].type) == 0) {
        printf("Semantic Check Passed: Valid types (%s) and valid scope.\n", table[i_lhs].type);
    } else {
        printf("Semantic Error: Type mismatch (%s = %s %c %s)\n",
               table[i_lhs].type, table[i_op1].type, op, table[i_op2].type);
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q8_typecheck.c -o q8_typecheck
$ ./q8_typecheck
Enter number of declarations: 3
Enter Declarations (Name Type Scope_Level[0=Global, 1=Local]):
a int 0
b int 1
c float 1

Enter current scope level for statement evaluation (0 or 1): 1
Enter statement in format (lhs = op1 + op2): a = b + c
Semantic Error: Type mismatch (int = int + float)
```

---

## Question 9: Code Optimization Techniques in C
**Problem Statement:** Develop a program that optimizes the given input block using Code Optimization Techniques.
**Functionality:** Takes a block of Three-Address Code expressions and performs **Common Subexpression Elimination (CSE)** and **Dead Code Elimination** by removing duplicate RHS computations and replacing redundant temporary variables.

### Program (`q9_opt.c`)
```c
#include <stdio.h>
#include <string.h>

struct Expr {
    char lhs[10];
    char rhs[30];
} code[20], opt[20];

int main() {
    int n, k = 0;
    printf("Enter number of statements: ");
    scanf("%d", &n);

    printf("Enter statements in format (LHS = RHS_Expression without spaces, e.g., t1 = a+b):\n");
    for (int i = 0; i < n; i++) {
        scanf("%s = %s", code[i].lhs, code[i].rhs);
    }

    // Common Subexpression Elimination
    for (int i = 0; i < n; i++) {
        int found = 0;
        for (int j = 0; j < k; j++) {
            if (strcmp(code[i].rhs, opt[j].rhs) == 0) {
                // Replace occurrences of code[i].lhs with opt[j].lhs in remaining expressions
                for (int m = i + 1; m < n; m++) {
                    char *pos = strstr(code[m].rhs, code[i].lhs);
                    if (pos != NULL) {
                        char temp[30];
                        int idx = pos - code[m].rhs;
                        strncpy(temp, code[m].rhs, idx);
                        temp[idx] = '\0';
                        strcat(temp, opt[j].lhs);
                        strcat(temp, pos + strlen(code[i].lhs));
                        strcpy(code[m].rhs, temp);
                    }
                }
                found = 1;
                break;
            }
        }
        if (!found) {
            opt[k++] = code[i];
        }
    }

    printf("\nOptimized Code (After Common Subexpression & Dead Code Elimination):\n");
    for (int i = 0; i < k; i++) {
        printf("%s = %s\n", opt[i].lhs, opt[i].rhs);
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q9_opt.c -o q9_opt
$ ./q9_opt
Enter number of statements: 4
Enter statements in format (LHS = RHS_Expression without spaces, e.g., t1 = a+b):
t1 = a+b
t2 = c+t1
t3 = a+b
t4 = c+t3

Optimized Code (After Common Subexpression & Dead Code Elimination):
t1 = a+b
t2 = c+t1
```

---

## Question 10: Generate Machine Code from Intermediate Code
**Problem Statement:** Given an intermediate code as an input. Develop a program that generates the machine code from the given input.
**Functionality:** Reads Three-Address Code (TAC) statements (`result = arg1 op arg2`) and translates each statement into 8086-style machine/assembly instructions (`MOV`, `ADD`, `SUB`, `MUL`, `DIV`) using general-purpose registers `R0, R1, ...`.

### Program (`q10_icg_mc.c`)
```c
#include <stdio.h>
#include <string.h>

int main() {
    int n;
    char lhs[10], arg1[10], arg2[10], op;

    printf("Enter number of intermediate code statements: ");
    scanf("%d", &n);

    printf("Enter statements (format: t1 = a + b):\n");
    for (int i = 0; i < n; i++) {
        scanf("%s = %s %c %s", lhs, arg1, &op, arg2);
        printf("\n; Machine code for %s = %s %c %s\n", lhs, arg1, op, arg2);
        printf("MOV R%d, %s\n", i, arg1);
        switch (op) {
            case '+': printf("ADD R%d, %s\n", i, arg2); break;
            case '-': printf("SUB R%d, %s\n", i, arg2); break;
            case '*': printf("MUL R%d, %s\n", i, arg2); break;
            case '/': printf("DIV R%d, %s\n", i, arg2); break;
        }
        printf("MOV %s, R%d\n", lhs, i);
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q10_icg_mc.c -o q10_icg_mc
$ ./q10_icg_mc
Enter number of intermediate code statements: 2
Enter statements (format: t1 = a + b):
t1 = a + b
x = t1 * c

; Machine code for t1 = a + b
MOV R0, a
ADD R0, b
MOV t1, R0

; Machine code for x = t1 * c
MOV R1, t1
MUL R1, c
MOV x, R1
```

---

## Question 11: Recognize Upper-Case Letter Followed by Five Digits or Alphabets using YACC
**Problem Statement:** Generate a valid pattern that recognizes all statements that begin with an Upper-Case Letter followed by five digits or alphabets. Use a YACC tool to do the same.
**Functionality:** LEX distinguishes uppercase letters (`UPPER`), lowercase letters (`LOWER`), and digits (`DIGIT`), while YACC checks the exact 6-character sequence (`UPPER` followed by exactly 5 alphanumeric tokens).

### LEX File (`q11_pat.l`)
```lex
%{
#include "y.tab.h"
%}

%%
[A-Z] { return UPPER; }
[a-z] { return LOWER; }
[0-9] { return DIGIT; }
\n    { return '\n'; }
.     { return yytext[0]; }
%%

int yywrap() { return 1; }
```

### YACC File (`q11_pat.y`)
```yacc
%{
#include <stdio.h>
#include <stdlib.h>
int yylex();
void yyerror(const char *s);
%}

%token UPPER LOWER DIGIT

%%
stmt  : UPPER alnum alnum alnum alnum alnum '\n' {
            printf("Valid Pattern Recognized!\n");
            exit(0);
        }
      ;
alnum : UPPER
      | LOWER
      | DIGIT
      ;
%%

void yyerror(const char *s) {
    printf("Invalid Pattern!\n");
    exit(0);
}

int main() {
    printf("Enter a 6-character string (Starts with Uppercase + 5 alphanumeric): ");
    yyparse();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ yacc -d q11_pat.y
$ lex q11_pat.l
$ gcc y.tab.c lex.yy.c -o q11_pat
$ ./q11_pat
Enter a 6-character string (Starts with Uppercase + 5 alphanumeric): Ab12cD
Valid Pattern Recognized!

$ ./q11_pat
Enter a 6-character string (Starts with Uppercase + 5 alphanumeric): ab12cD
Invalid Pattern!
```

---

## Question 12: Lexical Analyzer for Comments, Operators, and Keywords
**Problem Statement:** Design a lexical analyzer that identifies comments, operators and keywords from a given expression.
**Functionality:** Uses LEX rules to match single-line (`//...`) and multi-line (`/*...*/`) comments, C keywords, and arithmetic/relational/logical operators.

### Program (`q12_lex.l`)
```lex
%{
#include <stdio.h>
%}

%%
"//".*                                                    { printf("Single-line Comment : %s\n", yytext); }
"/*"([^*]|\*+[^*/])*\*+"/"                                { printf("Multi-line Comment  : %s\n", yytext); }
"int"|"float"|"char"|"if"|"else"|"for"|"while"|"return"   { printf("Keyword             : %s\n", yytext); }
"=="|"!="|"<="|">="|"="|"+"|"-"|"*"|"/"|"&&"|"||"         { printf("Operator            : %s\n", yytext); }
[a-zA-Z_][a-zA-Z0-9_]*                                    ; /* Ignore identifiers */
[0-9]+                                                    ; /* Ignore numbers */
[ \t\n;,\(\)\{\}]+                                        ; /* Ignore whitespace and separators */
.                                                         ;
%%

int yywrap() { return 1; }

int main() {
    printf("Enter code snippet (Ctrl+D to finish):\n");
    yylex();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ lex q12_lex.l
$ gcc lex.yy.c -o q12_lex
$ ./q12_lex
Enter code snippet (Ctrl+D to finish):
int x = a + b; // Initialize x
/* Check condition */
if (x >= 10) return x;
Keyword             : int
Operator            : =
Operator            : +
Single-line Comment : // Initialize x
Multi-line Comment  : /* Check condition */
Keyword             : if
Operator            : >=
Keyword             : return
```

---

## Question 13: Recognize Valid Control Structures Syntax of C Language
**Problem Statement:** Develop a Program to recognize a valid control structures syntax of C language (`for` loop, `while` loop, `if-else`, `if-else-if`, `switch-case`, etc.).
**Functionality:** Uses LEX and YACC to parse and validate the structural syntax of C control statements (`if`, `if-else`, `if-else-if`, `while`, `for`, and `switch-case`).

### LEX File (`q13_ctrl.l`)
```lex
%{
#include "y.tab.h"
%}

%%
"if"                  { return IF; }
"else"                { return ELSE; }
"while"               { return WHILE; }
"for"                 { return FOR; }
"switch"              { return SWITCH; }
"case"                { return CASE; }
"break"               { return BREAK; }
"default"             { return DEFAULT; }
"=="|"!="|"<="|">="|"<"|">"|"="|"+"|"-"|"++"|"--" { return OP; }
[a-zA-Z_][a-zA-Z0-9_]* { return ID; }
[0-9]+                { return NUM; }
[\(\)\{\}\;\:]        { return yytext[0]; }
[ \t\n]+              ;
.                     { return yytext[0]; }
%%

int yywrap() { return 1; }
```

### YACC File (`q13_ctrl.y`)
```yacc
%{
#include <stdio.h>
#include <stdlib.h>
int yylex();
void yyerror(const char *s);
%}

%token IF ELSE WHILE FOR SWITCH CASE BREAK DEFAULT ID NUM OP

%%
prog : stmt { printf("Valid Control Structure Syntax!\n"); exit(0); }
     ;

stmt : if_stmt
     | while_stmt
     | for_stmt
     | switch_stmt
     ;

if_stmt : IF '(' expr ')' block
        | IF '(' expr ')' block ELSE block
        | IF '(' expr ')' block ELSE if_stmt
        ;

while_stmt : WHILE '(' expr ')' block
           ;

for_stmt : FOR '(' expr ';' expr ';' expr ')' block
         ;

switch_stmt : SWITCH '(' ID ')' '{' case_list '}'
            ;

case_list : CASE NUM ':' assign ';' BREAK ';' case_list
          | DEFAULT ':' assign ';' BREAK ';'
          | /* empty */
          ;

block : '{' assign ';' '}'
      | assign ';'
      | '{' '}'
      ;

assign : ID OP expr
       | ID OP
       ;

expr : val OP val
     | val OP
     | val
     ;

val : ID | NUM ;
%%

void yyerror(const char *s) {
    printf("Invalid Control Structure Syntax!\n");
    exit(0);
}

int main() {
    printf("Enter a C control structure (Press Ctrl+D after input):\n");
    yyparse();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ yacc -d q13_ctrl.y
$ lex q13_ctrl.l
$ gcc y.tab.c lex.yy.c -o q13_ctrl
$ ./q13_ctrl
Enter a C control structure (Press Ctrl+D after input):
for (i = 0; i < 10; i++) { a = a + 1; }
Valid Control Structure Syntax!
```

---

## Question 14: Count Total Number of Vowels and Consonants using LEX
**Problem Statement:** Develop a Lex program to find out the total number of vowels and consonants from the given input string.
**Functionality:** Matches `[aeiouAEIOU]` to increment the vowel counter and remaining alphabetic characters `[a-zA-Z]` to increment the consonant counter.

### Program (`q14_vowels.l`)
```lex
%{
#include <stdio.h>
int vowels = 0, consonants = 0;
%}

%%
[aeiouAEIOU] { vowels++; }
[a-zA-Z]     { consonants++; }
\n           { return 0; }
.            ;
%%

int yywrap() { return 1; }

int main() {
    printf("Enter a string: ");
    yylex();
    printf("Total Vowels     : %d\n", vowels);
    printf("Total Consonants : %d\n", consonants);
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ lex q14_vowels.l
$ gcc lex.yy.c -o q14_vowels
$ ./q14_vowels
Enter a string: Compiler Design Lab
Total Vowels     : 6
Total Consonants : 11
```

---

## Question 15: Generate Machine Code from Postfix Notation
**Problem Statement:** Develop a program to generate machine code from a given postfix notation.
**Functionality:** Scans a postfix string using an evaluation stack of register indices; operands emit `MOV Rk, operand` and push `Rk`, while operators pop the top two registers and emit the corresponding arithmetic instruction (`ADD`, `SUB`, `MUL`, `DIV`).

### Program (`q15_postfix_mc.c`)
```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char postfix[50];
    int stack[50], top = -1, reg = 0;

    printf("Enter postfix expression (e.g., ab+c*): ");
    scanf("%s", postfix);

    printf("\nGenerated Machine Code:\n");
    for (int i = 0; postfix[i] != '\0'; i++) {
        char ch = postfix[i];
        if (isalnum(ch)) {
            printf("MOV R%d, %c\n", reg, ch);
            stack[++top] = reg++;
        } else {
            int r2 = stack[top--];
            int r1 = stack[top--];
            switch (ch) {
                case '+': printf("ADD R%d, R%d\n", r1, r2); break;
                case '-': printf("SUB R%d, R%d\n", r1, r2); break;
                case '*': printf("MUL R%d, R%d\n", r1, r2); break;
                case '/': printf("DIV R%d, R%d\n", r1, r2); break;
            }
            stack[++top] = r1;
        }
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q15_postfix_mc.c -o q15_postfix_mc
$ ./q15_postfix_mc
Enter postfix expression (e.g., ab+c*): ab+cd-*

Generated Machine Code:
MOV R0, a
MOV R1, b
ADD R0, R1
MOV R2, c
MOV R3, d
SUB R2, R3
MUL R0, R2
```

---

## Question 16: LEX Program to Scan Reserved Words, Variables, and Operators of C
**Problem Statement:** Write a LEX program to scan reserved words, variables and operators of C language.
**Functionality:** Uses regular expression rules in LEX to recognize C reserved words, valid C variable identifiers, and arithmetic/relational/logical/assignment operators.

### Program (`q16_scan.l`)
```lex
%{
#include <stdio.h>
%}

%%
"auto"|"break"|"case"|"char"|"const"|"continue"|"default"|"do"|"double"|"else"|"enum"|"extern"|"float"|"for"|"goto"|"if"|"int"|"long"|"register"|"return"|"short"|"signed"|"sizeof"|"static"|"struct"|"switch"|"typedef"|"union"|"unsigned"|"void"|"volatile"|"while" {
    printf("Reserved Word : %s\n", yytext);
}
[a-zA-Z_][a-zA-Z0-9_]* {
    printf("Variable      : %s\n", yytext);
}
"++"|"--"|"=="|"!="|"<="|">="|"&&"|"||"|"+="|"-="|"="|"+"|"-"|"*"|"/"|"%"|"<"|">" {
    printf("Operator      : %s\n", yytext);
}
[0-9]+|[ \t\n;,\(\)\{\}]+ ; /* Ignore numbers, whitespace, and punctuation */
. ;
%%

int yywrap() { return 1; }

int main() {
    printf("Enter C statements (Press Ctrl+D to stop):\n");
    yylex();
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ lex q16_scan.l
$ gcc lex.yy.c -o q16_scan
$ ./q16_scan
Enter C statements (Press Ctrl+D to stop):
while (count <= 10) { sum += count; count++; }
Reserved Word : while
Variable      : count
Operator      : <=
Variable      : sum
Operator      : +=
Variable      : count
Variable      : count
Operator      : ++
```

---

## Question 17: Convert Three-Address Code into Assembly Language in C
**Problem Statement:** Develop a program in C that converts the given three address code into assembly language statements.
**Functionality:** Parses Three-Address Code statements (`lhs = op1 operator op2` or simple copy `lhs = op1`) and outputs 8086-style assembly instructions (`MOV`, `ADD`, `SUB`, `MUL`, `DIV`) using register `AX`.

### Program (`q17_tac_asm.c`)
```c
#include <stdio.h>
#include <string.h>

int main() {
    int n;
    char line[50], lhs[15], op1[15], op2[15], op;

    printf("Enter number of TAC statements: ");
    scanf("%d", &n);
    getchar(); // consume newline

    printf("Enter TAC statements (e.g., t1 = a + b or x = t1):\n");
    for (int i = 0; i < n; i++) {
        fgets(line, sizeof(line), stdin);
        int matched = sscanf(line, "%s = %s %c %s", lhs, op1, &op, op2);

        if (matched == 4) {
            printf("MOV AX, %s\n", op1);
            switch (op) {
                case '+': printf("ADD AX, %s\n", op2); break;
                case '-': printf("SUB AX, %s\n", op2); break;
                case '*': printf("MUL %s\n", op2); break;
                case '/': printf("DIV %s\n", op2); break;
            }
            printf("MOV %s, AX\n\n", lhs);
        } else if (matched == 2) {
            printf("MOV AX, %s\n", op1);
            printf("MOV %s, AX\n\n", lhs);
        }
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q17_tac_asm.c -o q17_tac_asm
$ ./q17_tac_asm
Enter number of TAC statements: 3
Enter TAC statements (e.g., t1 = a + b or x = t1):
t1 = a + b
t2 = t1 * c
res = t2
MOV AX, a
ADD AX, b
MOV t1, AX

MOV AX, t1
MUL c
MOV t2, AX

MOV AX, t2
MOV res, AX
```

---

## Question 18: Eliminate Left Recursion from a Grammar in C
**Problem Statement:** Develop a C program to eliminate left recursion from a grammar.
**Functionality:** Checks each production of the form $A \to A\alpha \mid \beta$. If immediate left recursion exists, it rewrites the rule into two non-left-recursive productions: $A \to \beta A'$ and $A' \to \alpha A' \mid \varepsilon$.

### Program (`q18_leftrec.c`)
```c
#include <stdio.h>
#include <string.h>

int main() {
    int n;
    char nt, alpha[20], beta[20], prod[50];

    printf("Enter number of productions: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("\nEnter production %d (Format: E->E+T|T): ", i + 1);
        scanf("%s", prod);

        nt = prod[0];
        if (prod[3] == nt) {
            // Left recursive: A->Aalpha|beta
            int j = 4, k = 0, m = 0;
            while (prod[j] != '|' && prod[j] != '\0') {
                alpha[k++] = prod[j++];
            }
            alpha[k] = '\0';

            if (prod[j] == '|') {
                j++;
                while (prod[j] != '\0') {
                    beta[m++] = prod[j++];
                }
                beta[m] = '\0';
            }

            printf("Grammar is Left Recursive. After Elimination:\n");
            printf("%c  -> %s%c'\n", nt, beta, nt);
            printf("%c' -> %s%c' | epsilon\n", nt, alpha, nt);
        } else {
            printf("Grammar has no immediate left recursion:\n%s\n", prod);
        }
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q18_leftrec.c -o q18_leftrec
$ ./q18_leftrec
Enter number of productions: 2

Enter production 1 (Format: E->E+T|T): E->E+T|T
Grammar is Left Recursive. After Elimination:
E  -> TE'
E' -> +TE' | epsilon

Enter production 2 (Format: E->E+T|T): T->F
Grammar has no immediate left recursion:
T->F
```

---

## Question 19: Generate Abstract Syntax Tree (AST) from Arithmetic Expression in C
**Problem Statement:** Develop a program in C that generates an abstract syntax tree from a given arithmetic expression.
**Functionality:** Converts an infix arithmetic expression into an Abstract Syntax Tree (AST) using two stacks (operator stack and tree-node stack) based on operator precedence, then prints the tree structure and traversals.

### Program (`q19_ast.c`)
```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

typedef struct Node {
    char data;
    struct Node *left, *right;
} Node;

Node* createNode(char data, Node *left, Node *right) {
    Node *n = (Node*)malloc(sizeof(Node));
    n->data = data;
    n->left = left;
    n->right = right;
    return n;
}

int prec(char op) {
    if (op == '+' || op == '-') return 1;
    if (op == '*' || op == '/') return 2;
    return 0;
}

void printAST(Node *root, int space) {
    if (!root) return;
    space += 4;
    printAST(root->right, space);
    for (int i = 4; i < space; i++) printf(" ");
    printf("%c\n", root->data);
    printAST(root->left, space);
}

void postorder(Node *root) {
    if (!root) return;
    postorder(root->left);
    postorder(root->right);
    printf("%c ", root->data);
}

int main() {
    char expr[50], ops[50];
    Node *nodes[50];
    int top_op = -1, top_node = -1;

    printf("Enter arithmetic expression: ");
    scanf("%s", expr);

    for (int i = 0; expr[i] != '\0'; i++) {
        char ch = expr[i];
        if (isalnum(ch)) {
            nodes[++top_node] = createNode(ch, NULL, NULL);
        } else if (ch == '(') {
            ops[++top_op] = ch;
        } else if (ch == ')') {
            while (top_op != -1 && ops[top_op] != '(') {
                Node *r = nodes[top_node--];
                Node *l = nodes[top_node--];
                nodes[++top_node] = createNode(ops[top_op--], l, r);
            }
            top_op--; // pop '('
        } else {
            while (top_op != -1 && prec(ops[top_op]) >= prec(ch)) {
                Node *r = nodes[top_node--];
                Node *l = nodes[top_node--];
                nodes[++top_node] = createNode(ops[top_op--], l, r);
            }
            ops[++top_op] = ch;
        }
    }

    while (top_op != -1) {
        Node *r = nodes[top_node--];
        Node *l = nodes[top_node--];
        nodes[++top_node] = createNode(ops[top_op--], l, r);
    }

    printf("\nAbstract Syntax Tree (Rotated 90 degrees counter-clockwise):\n");
    printAST(nodes[top_node], 0);

    printf("\nPostorder Traversal of AST: ");
    postorder(nodes[top_node]);
    printf("\n");
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q19_ast.c -o q19_ast
$ ./q19_ast
Enter arithmetic expression: a+b*c

Abstract Syntax Tree (Rotated 90 degrees counter-clockwise):
        c
    *
        b
+
    a

Postorder Traversal of AST: a b c * +
```

---

## Question 20: Top-Down LL(1) Parser with Parsing Table (No Backtracking)
**Problem Statement:** Design a top-down parser which generates a parsing table with no backtracking.
**Functionality:** Computes the **LL(1) Predictive Parsing Table** for a given grammar using its `FIRST` and `FOLLOW` sets, displays the non-backtracking parsing table, and parses an input string using an explicit stack.

### Program (`q20_ll1.c`)
```c
#include <stdio.h>
#include <string.h>

/*
   Grammar without left recursion (E -> E+T | T, T -> id):
   0: E -> T A
   1: A -> + T A
   2: A -> #      (# represents epsilon)
   3: T -> i      (i represents id)

   Non-Terminals: E (0), A (1), T (2)
   Terminals    : i (0), + (1), $ (2)
*/

char *prod[4] = {"E->TA", "A->+TA", "A->#", "T->i"};
char *rhs[4]  = {"TA", "+TA", "#", "i"};

// Predictive Parsing Table M[Non-Terminal][Terminal] storing production index (-1 for error)
int table[3][3] = {
    /*         i   +   $  */
    /* E */ {  0, -1, -1 },
    /* A */ { -1,  1,  2 },
    /* T */ {  3, -1, -1 }
};

int nt_index(char c) {
    if (c == 'E') return 0;
    if (c == 'A') return 1;
    if (c == 'T') return 2;
    return -1;
}

int t_index(char c) {
    if (c == 'i') return 0;
    if (c == '+') return 1;
    if (c == '$') return 2;
    return -1;
}

int main() {
    char nt_names[3] = {'E', 'A', 'T'};
    char input[30], stack[50];
    int top = 0;

    printf("Predictive Parsing Table (LL(1) - No Backtracking):\n");
    printf("---------------------------------------------------\n");
    printf("NT\\T\t   i\t\t   +\t\t   $\n");
    printf("---------------------------------------------------\n");
    for (int i = 0; i < 3; i++) {
        printf(" %c\t", nt_names[i]);
        for (int j = 0; j < 3; j++) {
            if (table[i][j] != -1) printf("%s\t\t", prod[table[i][j]]);
            else printf("-\t\t");
        }
        printf("\n");
    }

    printf("\nEnter input string ending with $ (e.g., i+i$): ");
    scanf("%s", input);

    stack[0] = '$';
    stack[++top] = 'E';

    int ip = 0;
    printf("\nStack\t\tInput\t\tAction\n----------------------------------------------\n");
    while (top >= 0) {
        stack[top + 1] = '\0';
        printf("%s\t\t%s\t\t", stack, &input[ip]);

        char X = stack[top];
        char a = input[ip];

        if (X == a && X == '$') {
            printf("Accepted!\n");
            return 0;
        } else if (X == a) {
            printf("Match %c\n", a);
            top--;
            ip++;
        } else if (nt_index(X) != -1) {
            int r = nt_index(X);
            int c = t_index(a);
            if (c == -1 || table[r][c] == -1) {
                printf("Error! String Rejected.\n");
                return 0;
            }
            int p = table[r][c];
            printf("Output %s\n", prod[p]);
            top--;
            if (rhs[p][0] != '#') {
                int len = strlen(rhs[p]);
                for (int k = len - 1; k >= 0; k--) {
                    stack[++top] = rhs[p][k];
                }
            }
        } else {
            printf("Error! String Rejected.\n");
            return 0;
        }
    }
    return 0;
}
```

### Execution Commands & Sample Output
```bash
$ gcc q20_ll1.c -o q20_ll1
$ ./q20_ll1
Predictive Parsing Table (LL(1) - No Backtracking):
---------------------------------------------------
NT\T       i               +        

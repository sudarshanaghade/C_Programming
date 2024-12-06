//56. Accept book details of ‘n’ books viz, book title, author, publisher and cost. Assign an accession numbers to each book in increasing order. (Use dynamic memory allocation). Write a menu driven program for the following options. i. Books of a specific author ii. Books by a specific publisher iii. All books having cost >= _____ . iv. Information about a particular book (accept the title) v. All books. //

    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    // Structure to store book details
    typedef struct {
        int accession_number;
        char title[100];
        char author[100];
        char publisher[100];
        float cost;
        } Book;

    // Function prototypes
    void displayBooksByAuthor(Book *books, int n, const char *author);
    void displayBooksByPublisher(Book *books, int n, const char *publisher);
    void displayBooksByCost(Book *books, int n, float min_cost);
    void displayBookByTitle(Book *books, int n, const char *title);
    void displayAllBooks(Book *books, int n);

    int main() {
    int n, choice;
    char search_query[100];
    float min_cost;

    printf("Enter the number of books: ");
    scanf("%d", &n);
    getchar(); // Clear the newline character

    // Dynamic memory allocation for books
    Book *books = (Book *)malloc(n * sizeof(Book));
    if (books == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    // Input book details
    for (int i = 0; i < n; i++) {
        books[i].accession_number = i + 1;

        printf("\nEnter details for book %d:\n", i + 1);
        printf("Title: ");
        fgets(books[i].title, sizeof(books[i].title), stdin);
        books[i].title[strcspn(books[i].title, "\n")] = 0; // Remove newline

        printf("Author: ");
        fgets(books[i].author, sizeof(books[i].author), stdin);
        books[i].author[strcspn(books[i].author, "\n")] = 0;

        printf("Publisher: ");
        fgets(books[i].publisher, sizeof(books[i].publisher), stdin);
        books[i].publisher[strcspn(books[i].publisher, "\n")] = 0;

        printf("Cost: ");
        scanf("%f", &books[i].cost);
        getchar();
    }

    // Menu-driven program
    do {
        printf("\nMenu:\n");
        printf("1. Books of a specific author\n");
        printf("2. Books by a specific publisher\n");
        printf("3. All books having cost >= given value\n");
        printf("4. Information about a particular book (by title)\n");
        printf("5. Display all books\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // Clear newline character

        switch (choice) {
            case 1:
                printf("Enter author name: ");
                fgets(search_query, sizeof(search_query), stdin);
                search_query[strcspn(search_query, "\n")] = 0;
                displayBooksByAuthor(books, n, search_query);
                break;
            case 2:
                printf("Enter publisher name: ");
                fgets(search_query, sizeof(search_query), stdin);
                search_query[strcspn(search_query, "\n")] = 0;
                displayBooksByPublisher(books, n, search_query);
                break;
            case 3:
                printf("Enter minimum cost: ");
                scanf("%f", &min_cost);
                getchar();
                displayBooksByCost(books, n, min_cost);
                break;
            case 4:
                printf("Enter book title: ");
                fgets(search_query, sizeof(search_query), stdin);
                search_query[strcspn(search_query, "\n")] = 0;
                displayBookByTitle(books, n, search_query);
                break;
            case 5:
                displayAllBooks(books, n);
                break;
            case 6:
                printf("Exiting program.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 6);

    // Free allocated memory
    free(books);
    return 0;
    }
    
    
    
    void displayBooksByAuthor(Book *books, int n, const char *author) {
    int found = 0;
    printf("\nBooks by author '%s':\n", author);
    for (int i = 0; i < n; i++) {
        if (strcmp(books[i].author, author) == 0) {
            printf("Accession Number: %d, Title: %s, Publisher: %s, Cost: %.2f\n",
                   books[i].accession_number, books[i].title, books[i].publisher, books[i].cost);
            found = 1;
        }
    }
    if (!found) {
        printf("No books found by this author.\n");
    }
    }

    void displayBooksByPublisher(Book *books, int n, const char *publisher) {
    int found = 0;
    printf("\nBooks by publisher '%s':\n", publisher);
    for (int i = 0; i < n; i++) {
        if (strcmp(books[i].publisher, publisher) == 0) {
            printf("Accession Number: %d, Title: %s, Author: %s, Cost: %.2f\n",
                   books[i].accession_number, books[i].title, books[i].author, books[i].cost);
            found = 1;
        }
    }
    if (!found) {
        printf("No books found by this publisher.\n");
    }
    }

    void displayBooksByCost(Book *books, int n, float min_cost) {
    int found = 0;
    printf("\nBooks with cost >= %.2f:\n", min_cost);
    for (int i = 0; i < n; i++) {
        if (books[i].cost >= min_cost) {
            printf("Accession Number: %d, Title: %s, Author: %s, Publisher: %s, Cost: %.2f\n",
                   books[i].accession_number, books[i].title, books[i].author, books[i].publisher, books[i].cost);
            found = 1;
        }
    }
    if (!found) {
        printf("No books found with cost >= %.2f.\n", min_cost);
    }
    }

    void displayBookByTitle(Book *books, int n, const char *title) {
    int found = 0;
    printf("\nInformation about book titled '%s':\n", title);
    for (int i = 0; i < n; i++) {
        if (strcmp(books[i].title, title) == 0) {
            printf("Accession Number: %d, Author: %s, Publisher: %s, Cost: %.2f\n",
                   books[i].accession_number, books[i].author, books[i].publisher, books[i].cost);
            found = 1;
            break;
        }
    }
    if (!found) {
        printf("No book found with the given title.\n");
    }
    }

    void displayAllBooks(Book *books, int n) {
    printf("\nAll books:\n");
    for (int i = 0; i < n; i++) {
        printf("Accession Number: %d, Title: %s, Author: %s, Publisher: %s, Cost: %.2f\n",
               books[i].accession_number, books[i].title, books[i].author, books[i].publisher, books[i].cost);
    }
    }

// 55. Create a structure employee (id, name, salary). Accept details of n 
 employees and write a menu driven program to perform the following 
  operations. Write separate functions for the 
different options.  i) Search by name 
ii) Search by id 
iii) Display all 
iv) Display all employees having salary > _____ 
v) Display employee having maximum salary. //

    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>

    // Structure to store employee details
        typedef struct {
    int id;
    char name[100];
    float salary;
                } Employee;

    // Function prototypes
    void searchByName(Employee *employees, int n, const char *name);
    void searchById(Employee *employees, int n, int id);
    void displayAllEmployees(Employee *employees, int n);
    void displayEmployeesBySalary(Employee *employees, int n, float min_salary);
    void displayEmployeeWithMaxSalary(Employee *employees, int n);

    int main() {
    int n, choice, id;
    char search_query[100];
    float min_salary;

    printf("Enter the number of employees: ");
    scanf("%d", &n);
    getchar(); // Clear the newline character

    // Dynamic memory allocation for employees
    Employee *employees = (Employee *)malloc(n * sizeof(Employee));
    if (employees == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    // Input employee details
    for (int i = 0; i < n; i++) {
        printf("\nEnter details for employee %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &employees[i].id);
        getchar();

        printf("Name: ");
        fgets(employees[i].name, sizeof(employees[i].name), stdin);
        employees[i].name[strcspn(employees[i].name, "\n")] = 0;

        printf("Salary: ");
        scanf("%f", &employees[i].salary);
        getchar();
    }

    // Menu-driven program
    do {
        printf("\nMenu:\n");
        printf("1. Search by name\n");
        printf("2. Search by ID\n");
        printf("3. Display all employees\n");
        printf("4. Display all employees having salary > given value\n");
        printf("5. Display employee with maximum salary\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // Clear newline character

        switch (choice) {
            case 1:
                printf("Enter name: ");
                fgets(search_query, sizeof(search_query), stdin);
                search_query[strcspn(search_query, "\n")] = 0;
                searchByName(employees, n, search_query);
                break;
            case 2:
                printf("Enter ID: ");
                scanf("%d", &id);
                getchar();
                searchById(employees, n, id);
                break;
            case 3:
                displayAllEmployees(employees, n);
                break;
            case 4:
                printf("Enter minimum salary: ");
                scanf("%f", &min_salary);
                getchar();
                displayEmployeesBySalary(employees, n, min_salary);
                break;
            case 5:
                displayEmployeeWithMaxSalary(employees, n);
                break;
            case 6:
                printf("Exiting program.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 6);

    // Free allocated memory
    free(employees);
    return 0;
    }

    void searchByName(Employee *employees, int n, const char *name) {
    int found = 0;
    printf("\nEmployees with name '%s':\n", name);
    for (int i = 0; i < n; i++) {
        if (strcmp(employees[i].name, name) == 0) {
            printf("ID: %d, Name: %s, Salary: %.2f\n",
                   employees[i].id, employees[i].name, employees[i].salary);
            found = 1;
        }
    }
    if (!found) {
        printf("No employees found with the given name.\n");
    }
    }

    void searchById(Employee *employees, int n, int id) {
    int found = 0;
    printf("\nEmployee with ID %d:\n", id);
    for (int i = 0; i < n; i++) {
        if (employees[i].id == id) {
            printf("ID: %d, Name: %s, Salary: %.2f\n",
                   employees[i].id, employees[i].name, employees[i].salary);
            found = 1;
            break;
        }
    }
    if (!found) {
        printf("No employee found with the given ID.\n");
    }
    }

    void displayAllEmployees(Employee *employees, int n) {
    printf("\nAll employees:\n");
    for (int i = 0; i < n; i++) {
        printf("ID: %d, Name: %s, Salary: %.2f\n",
               employees[i].id, employees[i].name, employees[i].salary);
    }
    }

    void displayEmployeesBySalary(Employee *employees, int n, float min_salary) {
    int found = 0;
    printf("\nEmployees with salary > %.2f:\n", min_salary);
    for (int i = 0; i < n; i++) {
        if (employees[i].salary > min_salary) {
            printf("ID: %d, Name: %s, Salary: %.2f\n",
                   employees[i].id, employees[i].name, employees[i].salary);
            found = 1;
        }
    }
    if (!found) {
        printf("No employees found with salary > %.2f.\n", min_salary);
    }
    }

    void displayEmployeeWithMaxSalary(Employee *employees, int n) {
    if (n <= 0) {
        printf("No employees available to find maximum salary.\n");
        return;
            }

    int max_index = 0;
    for (int i = 1; i < n; i++) {
        if (employees[i].salary > employees[max_index].salary) {
            max_index = i;
        }
    }

    printf("\nEmployee with maximum salary:\n");
    printf("ID: %d, Name: %s, Salary: %.2f\n",
           employees[max_index].id, employees[max_index].name, employees[max_index].salary);
    }


//54. Create a structure student (roll number, name, marks of 3 subjects, 
percentage). Accept 
details of n students and write a menu driven program to perform the 
following operations. Write separate functions for the different 
options. 
i) Search 
ii) Display all student details 
iii) Display all student having percentage > _____ 
v) Display student having maximum percentage .


        #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>

    // Structure to store student details
    typedef struct {
    int rollNumber;
    char name[100];
    float marks[3];
    float percentage;
    } Student;

    // Function prototypes
    void searchStudent(Student *students, int n, const char *name);
    void displayAllStudents(Student *students, int n);
    void displayStudentsByPercentage(Student *students, int n, float min_percentage);
    void displayStudentWithMaxPercentage(Student *students, int n);

    int main() {
    int n, choice;
    char search_query[100];
    float min_percentage;

    printf("Enter the number of students: ");
    scanf("%d", &n);
    getchar(); // Clear the newline character

    // Dynamic memory allocation for students
    Student *students = (Student *)malloc(n * sizeof(Student));
    if (students == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    // Input student details
    for (int i = 0; i < n; i++) {
        printf("\nEnter details for student %d:\n", i + 1);
        printf("Roll Number: ");
        scanf("%d", &students[i].rollNumber);
        getchar();

        printf("Name: ");
        fgets(students[i].name, sizeof(students[i].name), stdin);
        students[i].name[strcspn(students[i].name, "\n")] = 0;

        printf("Enter marks of 3 subjects: ");
        for (int j = 0; j < 3; j++) {
            scanf("%f", &students[i].marks[j]);
        }

        // Calculate percentage
        students[i].percentage = (students[i].marks[0] + students[i].marks[1] + students[i].marks[2]) / 3;
    }

    // Menu-driven program
    do {
        printf("\nMenu:\n");
        printf("1. Search by name\n");
        printf("2. Display all students\n");
        printf("3. Display all students having percentage > given value\n");
        printf("4. Display student with maximum percentage\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // Clear newline character

        switch (choice) {
            case 1:
                printf("Enter name: ");
                fgets(search_query, sizeof(search_query), stdin);
                search_query[strcspn(search_query, "\n")] = 0;
                searchStudent(students, n, search_query);
                break;
            case 2:
                displayAllStudents(students, n);
                break;
            case 3:
                printf("Enter minimum percentage: ");
                scanf("%f", &min_percentage);
                getchar();
                displayStudentsByPercentage(students, n, min_percentage);
                break;
            case 4:
                displayStudentWithMaxPercentage(students, n);
                break;
            case 5:
                printf("Exiting program.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 5);

    // Free allocated memory
    free(students);
    return 0;
    }

    void searchStudent(Student *students, int n, const char *name) {
    int found = 0;
    printf("\nStudents with name '%s':\n", name);
    for (int i = 0; i < n; i++) {
        if (strcmp(students[i].name, name) == 0) {
            printf("Roll Number: %d, Name: %s, Percentage: %.2f\n",
                   students[i].rollNumber, students[i].name, students[i].percentage);
            found = 1;
        }
    }
    if (!found) {
        printf("No students found with the given name.\n");
    }
    }

    void displayAllStudents(Student *students, int n) {
    printf("\nAll students:\n");
    for (int i = 0; i < n; i++) {
        printf("Roll Number: %d, Name: %s, Marks: %.2f, %.2f, %.2f, Percentage: %.2f\n",
               students[i].rollNumber, students[i].name, students[i].marks[0],
               students[i].marks[1], students[i].marks[2], students[i].percentage);
    }
    }

    void displayStudentsByPercentage(Student *students, int n, float min_percentage) {
    int found = 0;
    printf("\nStudents with percentage > %.2f:\n", min_percentage);
    for (int i = 0; i < n; i++) {
        if (students[i].percentage > min_percentage) {
            printf("Roll Number: %d, Name: %s, Percentage: %.2f\n",
                   students[i].rollNumber, students[i].name, students[i].percentage);
            found = 1;
        }
    }
    if (!found) {
        printf("No students found with percentage > %.2f.\n", min_percentage);
    }
    }

    void displayStudentWithMaxPercentage(Student *students, int n) {
    if (n <= 0) {
        printf("No students available to find maximum percentage.\n");
        return;
        }

    int max_index = 0;
    for (int i = 1; i < n; i++) {
        if (students[i].percentage > students[max_index].percentage) {
            max_index = i;
        }
    }

    printf("\nStudent with maximum percentage:\n");
    printf("Roll Number: %d, Name: %s, Percentage: %.2f\n",
           students[max_index].rollNumber, students[max_index].name, students[max_index].percentage);
    }


//53. Write a program to find the frequency of the character in the given 
string. //

        #include <stdio.h>
        #include <string.h>

    void findFrequency(const char *str) {
    int freq[256] = {0}; // Array to store the frequency of characters

    // Calculate frequency of each character
    for (int i = 0; str[i] != '\0'; i++) {
        freq[(unsigned char)str[i]]++;
    }

    // Display the frequency of characters
    printf("Character frequencies:\n");
    for (int i = 0; i < 256; i++) {
        if (freq[i] > 0) {
            printf("%c: %d\n", i, freq[i]);
        }
    }
    }

    int main() {
    char str[1000];

    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; // Remove newline character

    findFrequency(str);

    return 0;
    }

// 52. Write a program which accepts a sentence from the user and alters 
 it as follows: Every space is replaced by *, case of all alphabets is 
reversed, digits are replaced by ?//

    #include <stdio.h>
    #include <ctype.h>
    #include <string.h>

    void alterSentence(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] == ' ') {
            str[i] = '*'; // Replace spaces with '*'
        } else if (isalpha(str[i])) {
            if (islower(str[i])) {
                str[i] = toupper(str[i]); // Convert lowercase to uppercase
            } else {
                str[i] = tolower(str[i]); // Convert uppercase to lowercase
            }
        } else if (isdigit(str[i])) {
            str[i] = '?'; // Replace digits with '?'
        }
    }
    }

    int main() {
    char str[1000];

    printf("Enter a sentence: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; // Remove newline character

    alterSentence(str);

    printf("Altered sentence: %s\n", str);

    return 0;
    }

// 51. For the following standard functions, write corresponding user 
defined functions and write a menu driven program to use them. 
strcat, strcmp, strrev, strupr //

    #include <stdio.h>
    #include <string.h>
    #include <ctype.h>

    // User-defined strcat function
    void myStrcat(char *dest, const char *src) {
    while (*dest) dest++; // Move to the end of dest
    while ((*dest++ = *src++)); // Copy src to dest
    }

    // User-defined strcmp function
    int myStrcmp(const char *str1, const char *str2) {
    while (*str1 && (*str1 == *str2)) {
        str1++;
        str2++;
    }
    return *(unsigned char *)str1 - *(unsigned char *)str2;
    }

    // User-defined strrev function
    void myStrrev(char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - i - 1];
        str[len - i - 1] = temp;
    }
    }

        // User-defined strupr function
    void myStrupr(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (islower(str[i])) {
            str[i] = toupper(str[i]);
        }
    }
    }

    int main() {
    char str1[100], str2[100], choice;

    do {
        printf("\nMenu:\n");
        printf("1. Concatenate strings (strcat)\n");
        printf("2. Compare strings (strcmp)\n");
        printf("3. Reverse string (strrev)\n");
        printf("4. Convert to uppercase (strupr)\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);
        getchar(); // Clear newline character

        switch (choice) {
            case '1':
                printf("Enter first string: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0; // Remove newline character
                printf("Enter second string: ");
                fgets(str2, sizeof(str2), stdin);
                str2[strcspn(str2, "\n")] = 0;
                myStrcat(str1, str2);
                printf("Concatenated string: %s\n", str1);
                break;

            case '2':
                printf("Enter first string: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                printf("Enter second string: ");
                fgets(str2, sizeof(str2), stdin);
                str2[strcspn(str2, "\n")] = 0;
                int cmp_result = myStrcmp(str1, str2);
                if (cmp_result == 0) {
                    printf("Strings are equal.\n");
                } else if (cmp_result < 0) {
                    printf("First string is less than second string.\n");
                } else {
                    printf("First string is greater than second string.\n");
                }
                break;

            case '3':
                printf("Enter a string to reverse: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                myStrrev(str1);
                printf("Reversed string: %s\n", str1);
                break;

            case '4':
                printf("Enter a string to convert to uppercase: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                myStrupr(str1);
                printf("Uppercase string: %s\n", str1);
                break;

            case '5':
                printf("Exiting program.\n");
                break;

            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != '5');

    return 0;
    }


// 50. A palindrome is a string that reads the same-forward and reverse. 
Example: “madam” is a Palindrome. Write a function which accepts a 
string and returns 1 if the string is a palindrome and 0 otherwise. Use 
this function in main. //

    #include <stdio.h>
    #include <string.h>
    #include <ctype.h>

    // User-defined strcat function
    void myStrcat(char *dest, const char *src) {
    while (*dest) dest++; // Move to the end of dest
    while ((*dest++ = *src++)); // Copy src to dest
    }

    // User-defined strcmp function
    int myStrcmp(const char *str1, const char *str2) {
    while (*str1 && (*str1 == *str2)) {
        str1++;
        str2++;
    }
    return *(unsigned char *)str1 - *(unsigned char *)str2;
        }

    // User-defined strrev function
    void myStrrev(char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - i - 1];
        str[len - i - 1] = temp;
    }
    }

    // User-defined strupr function
    void myStrupr(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (islower(str[i])) {
            str[i] = toupper(str[i]);
        }
    }
    }

    // Function to check if a string is a palindrome
    int isPalindrome(const char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        if (str[i] != str[len - i - 1]) {
            return 0; // Not a palindrome
        }
    }
    return 1; // Palindrome
    }

    int main() {
    char str1[100], str2[100], choice;

    do {
        printf("\nMenu:\n");
        printf("1. Concatenate strings (strcat)\n");
        printf("2. Compare strings (strcmp)\n");
        printf("3. Reverse string (strrev)\n");
        printf("4. Convert to uppercase (strupr)\n");
        printf("5. Check if a string is a palindrome\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);
        getchar(); // Clear newline character

        switch (choice) {
            case '1':
                printf("Enter first string: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0; // Remove newline character
                printf("Enter second string: ");
                fgets(str2, sizeof(str2), stdin);
                str2[strcspn(str2, "\n")] = 0;
                myStrcat(str1, str2);
                printf("Concatenated string: %s\n", str1);
                break;

            case '2':
                printf("Enter first string: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                printf("Enter second string: ");
                fgets(str2, sizeof(str2), stdin);
                str2[strcspn(str2, "\n")] = 0;
                int cmp_result = myStrcmp(str1, str2);
                if (cmp_result == 0) {
                    printf("Strings are equal.\n");
                } else if (cmp_result < 0) {
                    printf("First string is less than second string.\n");
                } else {
                    printf("First string is greater than second string.\n");
                }
                break;

            case '3':
                printf("Enter a string to reverse: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                myStrrev(str1);
                printf("Reversed string: %s\n", str1);
                break;

            case '4':
                printf("Enter a string to convert to uppercase: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                myStrupr(str1);
                printf("Uppercase string: %s\n", str1);
                break;

            case '5':
                printf("Enter a string to check if it is a palindrome: ");
                fgets(str1, sizeof(str1), stdin);
                str1[strcspn(str1, "\n")] = 0;
                if (isPalindrome(str1)) {
                    printf("The string is a palindrome.\n");
                } else {
                    printf("The string is not a palindrome.\n");
                }
                break;

            case '6':
                printf("Exiting program.\n");
                break;

            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != '6');

    return 0;
    }

// 49. Write a program that will accept a string and character to search. 
The program will call a function, which will search for the occurrence 
position of the character in the string and return its position. Function 
should return –1 if the character is not found in the string.// 

        #include <stdio.h>
        #include <string.h>
        #include <ctype.h>

    // Function to search for a character in a string and return its position
    int findCharPosition(const char *str, char ch) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] == ch) {
            return i; // Return position if character is found
        }
    }
    return -1; // Return -1 if character is not found
        }

    int main() {
    char str[100], ch;
    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; // Remove newline character

    printf("Enter a character to search: ");
    scanf(" %c", &ch);

    int position = findCharPosition(str, ch);

    if (position != -1) {
        printf("The character '%c' is found at position %d.\n", ch, position);
    } else {
        printf("The character '%c' is not found in the string.\n", ch);
    }

    return 0;
    }

//48. Write a program to allocate memory dynamically for n integers 
such that the memory is initialized to 0. Accept the data from the user 
and find the range of the data elements.//

    #include <stdio.h>
    #include <stdlib.h>

    // Function to find the range of data elements
    void findRange(int *arr, int n, int *min, int *max) {
    *min = *max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < *min) {
            *min = arr[i];
        }
        if (arr[i] > *max) {
            *max = arr[i];
        }
    }
    }

    int main() {
    int n;
    printf("Enter the number of integers: ");
    scanf("%d", &n);

    // Allocate memory dynamically and initialize to 0
    int *arr = (int *)calloc(n, sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    printf("Enter %d integers: \n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int min, max;
    findRange(arr, n, &min, &max);

    printf("The range of the data elements is: %d to %d\n", min, max);

    // Free the allocated memory
    free(arr);

    return 0;
    }
    
//47. Write a program to display the elements of an array containing n
integers in the reverse order using a pointer to the array.//

    #include <stdio.h>

    int main() {
    int n, i;

    printf("Enter the number of elements: ");
    scanf("%d", &n);

    int arr[n];

    printf("Enter the elements of the array:\n");
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int *ptr = &arr[n - 1]; // Pointer to the last element

    printf("Elements in reverse order:\n");
    for (i = n - 1; i >= 0; i--) {
        printf("%d ", *ptr);
        ptr--; // Move the pointer to the previous element
    }

    printf("\n");

    return 0;
    }

// 46. Write a function which takes hours, minutes and seconds as
parameters and an integer s and increments the time by s seconds.
Accept time and seconds in main and Display the new time in main
using the above function.//

    #include <stdio.h>
    void increment_time(int *hours, int *minutes, int *seconds, int s) {
    int total_seconds = (*hours * 3600) + (*minutes * 60) + *seconds + s;

    *seconds = total_seconds % 60;
    total_seconds /= 60;

    *minutes = total_seconds % 60;
    *hours = total_seconds / 60;
    }

    int main() {
    int hours, minutes, seconds, s;

    printf("Enter the time (hours, minutes, seconds): ");
    scanf("%d %d %d", &hours, &minutes, &seconds);

    printf("Enter the number of seconds to increment: ");
    scanf("%d", &s);

    increment_time(&hours, &minutes, &seconds, s);

    printf("New time: %02d:%02d:%02d\n", hours, minutes, seconds);

    return 0;
    }

//45. Write a program to add and multiply two matrices. Write separate 
functions to accept, display, add and multiply the matrices. Perform 
necessary checks before adding and multiplying the matrices.//

    #include <stdio.h>

    void accept_matrix(int rows, int cols, int matrix[rows][cols]) {
    printf("Enter elements of the matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
    }

    void display_matrix(int rows, int cols, int matrix[rows][cols]) {
    printf("Matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    }

    void add_matrices(int rows, int cols, int matrix1[rows][cols], int matrix2[rows][cols], int result[rows][cols]) {
    if (rows != rows || cols != cols) {
        printf("Matrices cannot be added. Dimensions do not match.\n");
        return;
    }

    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            result[i][j] = matrix1[i][j] + matrix2[i][j];
        }
    }
    }

    void multiply_matrices(int rows1, int cols1, int matrix1[rows1][cols1], int rows2, int cols2, int matrix2[rows2][cols2], int result[rows1][cols2]) {
    if (cols1 != rows2) {
        printf("Matrices cannot be multiplied. Number of columns in the first matrix must equal the number of rows in the second matrix.\n");
        return;
    }

    for (int i = 0; i < rows1; i++) {
        for (int j = 0; j < cols2; j++) {
            result[i][j] = 0;
            for (int k = 0; k < cols1; k++) {
                result[i][j] += matrix1[i][k] * matrix2[k][j];
            }
        }
    }
    }

    int main() {
    int rows1, cols1, rows2, cols2;

    printf("Enter the dimensions of the first matrix (rows, columns): ");
    scanf("%d %d", &rows1, &cols1);

    int matrix1[rows1][cols1];
    accept_matrix(rows1, cols1, matrix1);

    printf("Enter the dimensions of the second matrix (rows, columns): ");
    scanf("%d %d", &rows2, &cols2);

    int matrix2[rows2][cols2];
    accept_matrix(rows2, cols2, matrix2);

    printf("\nMatrix 1:\n");
    display_matrix(rows1, cols1, matrix1);

    printf("\nMatrix 2:\n");
    display_matrix(rows2, cols2, matrix2);

    int sum_matrix[rows1][cols1];
    add_matrices(rows1, cols1, matrix1, rows2, cols2, sum_matrix);

    if (rows1 == rows2 && cols1 == cols2) {
        printf("\nSum of matrices:\n");
        display_matrix(rows1, cols1, sum_matrix);
    }

    int product_matrix[rows1][cols2];
    multiply_matrices(rows1, cols1, matrix1, rows2, cols2, product_matrix);

    if (cols1 == rows2) {
        printf("\nProduct of matrices:\n");
        display_matrix(rows1, cols2, product_matrix);
    }

    return 0;
    }

//44. Write a program to accept a matrix A of size m x n and store its 
transpose in matrix B. Display matrix B. Write separate functions. //

    #include <stdio.h>

    void accept_matrix(int rows, int cols, int matrix[rows][cols]) {
    printf("Enter elements of the matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
    }

    void display_matrix(int rows, int cols, int matrix[rows][cols]) {
    printf("Matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    }

    void transpose_matrix(int rows, int cols, int matrix[rows][cols], int transpose[cols][rows]) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            transpose[j][i] = matrix[i][j];
        }
    }
    }

    int main() {
    int rows, cols;

    printf("Enter the dimensions of the matrix (rows, columns): ");
    scanf("%d %d", &rows, &cols);

    int matrix[rows][cols];
    accept_matrix(rows, cols, matrix);

    printf("\nOriginal Matrix:\n");
    display_matrix(rows, cols, matrix);

    int transpose[cols][rows];
    transpose_matrix(rows, cols, matrix, transpose);

    printf("\nTranspose Matrix:\n");
    display_matrix(cols, rows, transpose);

    return 0;
    }


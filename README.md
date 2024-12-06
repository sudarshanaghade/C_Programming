#56. Accept book details of ‘n’ books viz, book title, author, publisher and cost. Assign an accession numbers to each book in increasing order. (Use dynamic memory allocation). Write a menu driven program for the following options. i. Books of a specific author ii. Books by a specific publisher iii. All books having cost >= _____ . iv. Information about a particular book (accept the title) v. All books. 


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

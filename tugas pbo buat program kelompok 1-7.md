~~~dart
import 'dart:io';
void main() {
  List<String> books = ['The Great Gatsby', '1984', 'To Kill a Mockingbird'];
  List<bool> availability = [true, true, true]; // true means available, false means borrowed
  
  void displayBooks() {
    print('\nAvailable Books:');
    for (int i = 0; i < books.length; i++) {
      if (availability[i]) {
        print('${i + 1}. ${books[i]}');
      }
    }
  }

  void borrowBook() {
    displayBooks();
    stdout.write('Enter the number of the book you want to borrow: ');
    int bookIndex = int.parse(stdin.readLineSync()!) - 1;
    
    if (bookIndex >= 0 && bookIndex < books.length && availability[bookIndex]) {
      availability[bookIndex] = false;
      print('You have borrowed "${books[bookIndex]}".');
    } else {
      print('Invalid choice or the book is not available.');
    }
  }

  void returnBook() {
    stdout.write('Enter the name of the book you want to return: ');
    String bookName = stdin.readLineSync()!;
    
    int index = books.indexOf(bookName);
    if (index != -1 && !availability[index]) {
      availability[index] = true;
      print('You have returned "${books[index]}".');
    } else {
      print('Invalid book name or the book was not borrowed.');
    }
  }

  void displayMenu() {
    print('\nLibrary Menu:');
    print('1. Display Available Books');
    print('2. Borrow a Book');
    print('3. Return a Book');
    print('4. Exit');
  }

  while (true) {
    displayMenu();
    stdout.write('Select an option: ');
    int choice = int.parse(stdin.readLineSync()!);

    switch (choice) {
      case 1:
        displayBooks();
        break;
      case 2:
        borrowBook();
        break;
      case 3:
        returnBook();
        break;
      case 4:
        print('Thank you for using the library system!');
        return;
      default:
        print('Invalid option. Please try again.');
    }
  }
}
~~~
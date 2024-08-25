#include <iostream>
#include <string>
#include <direct.h>
#include <dos.h>

using namespace std;

void list_files() {
    system("di");
}

void list_files_extension(string ext) {
    system("di *.");
}

void list_files_pattern(string pattern) {
    system("dir" + pattern);
}

void create_directory() {
    string di_name;
    cout << "Enter directory name: ";
    getline(cin, di_name);
    if (_mkdir(di_name.c_str()) == 0) {
        cout << "Directory created successfully: " << dir_name << endl;
    } else {
        cout << "Error creating directory: " << di_name << endl;
    }
}

void change_directory() {
    int choice;
    cout << "Enter your choice:" << endl;
    cout << "1. Move one step back (to the parent directory)." << endl;
    cout << "2. Move to the root directory." << endl;
    cout << "3. Move to a specific directory." << endl;
    cin >> choice;

    switch (choice) {
        case 1:
            if (_chdir("..") == 0) {
                cout << "Moved to parent directory successfully." << endl;
            } else {
                cout << "Error moving to parent directory." << endl;
            }
            break;
        case 2:
            if (_chdir("/") == 0) {
                cout << "Moved to root directory successfully." << endl;
            } else {
                cout << "Error moving to root directory." << endl;
            }
            break;
        case 3:
            string dir_name;
            cout << "Enter directory name: ";
            getline(cin, dir_name);
            if (_chdir(dir_name.c_str()) == 0) {
                cout << "Moved to directory successfully: " << dir_name <<            } else {
                cout << "Error moving to directory: " << dir_name << endl;
            }
            break;
        default:
            cout << "Invalid choice." << endl;
            break;
    }
}

void exit_program() {
    cout << "Exiting program." << endl;
    exit(0);
}

void main_menu() {
    int choice;
    cout << "Directory Management System" << endl;
    cout << "1. List files in the current directory." << endl;
    cout << "2. Create a new directory." << endl;
    cout << "3. Change the working directory." << endl;
    cout << "4. Exit the program." << endl;
    cout << "Enter your choice:" << endl;
    cin >> choice;

    switch (choice) {
        case 1:
            list_files();
            break;
        case 2:
            create_directory();
            break;
        case 3:
            change_directory();
            break;
        case 4:
            exit_program();
            break;
        default:
            cout << "Invalid choice." << endl;
            break;
    }

    main_menu();
}

int main() {
    main_menu return 0;
}

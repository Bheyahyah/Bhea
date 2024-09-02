#include <iostream>
#include <filesystem>
#include <string>

namespace fs = std::filesystem;


void listFiles(const fs::path& dir) {
    try {
        if (!fs::exists(dir)) {
            std::cerr << "Error: Directory does not exist.\n";
            return;
        }
        std::cout << "Listing files in directory: " << dir << std::endl;
        for (const auto& entry : fs::directory_iterator(dir)) {
            std::cout << (entry.is_directory() ? "[DIR] " : "[FILE] ")
                      << entry.path().filename().string() << std::endl;
        }
    } catch (const fs::filesystem_error& e) {
        std::cerr << "Filesystem error: " << e.what() << std::endl;
    }
}


void createDirectory(const fs::path& dir) {
    try {
        if (fs::create_directory(dir)) {
            std::cout << "Directory '" << dir << "' created successfully.\n";
        } else {
            std::cerr << "Error: Failed to create directory. It may already exist.\n";
        }
    } catch (const fs::filesystem_error& e) {
        std::cerr << "Filesystem error: " << e.what() << std::endl;
    }
}


void changeDirectory(fs::path& currentPath, const fs::path& newDir) {
    try {
        if (fs::exists(newDir) && fs::is_directory(newDir)) {
            currentPath = newDir;
            std::cout << "Directory changed to: " << currentPath << std::endl;
        } else {
            std::cerr << "Error: Directory does not exist or is not valid.\n";
        }
    } catch (const fs::filesystem_error& e) {
        std::cerr << "Filesystem error: " << e.what() << std::endl;
    }
}


void displayMenu() {
    std::cout << "\nDirectory Management System\n";
    std::cout << "1. List Files\n";
    std::cout << "2. Create Directory\n";
    std::cout << "3. Change Directory\n";
    std::cout << "4. Exit\n";
    std::cout << "Enter your choice: ";
}

int main() {
    fs::path currentPath = fs::current_path();
    int choice;
    std::string input;

    while (true) {
        std::cout << "Current Directory: " << currentPath << "\n";
        displayMenu();
        std::cin >> choice;

        switch (choice) {
            case 1:
                listFiles(currentPath);
                break;
            case 2:
                std::cout << "Enter the name of the directory to create: ";
                std::cin >> input;
                createDirectory(currentPath / input);
                break;
            case 3:
                std::cout << "Enter the path of the directory to change to: ";
                std::cin >> input;
                changeDirectory(currentPath, input);
                break;
            case 4:
                std::cout << "Exiting the program.\n";
                return 0;
            default:
                std::cerr << "Invalid choice. Please try again.\n";
                break;
        }
    }

    return 0;
    

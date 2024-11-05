#include <iostream>
#include <string>

using namespace std;

struct Expense {
    string name;
    double cost;
};

class Tracker {
public:
    Tracker() : count(0) {}

    // Add an expense
    void add(string item, double price) {
        if (count < MAX) {
            list[count].name = item;
            list[count].cost = price;
            count++;
            cout << "Added: " << item << " - ₹ " << price << endl;
        } else {
            cout << "No more space to add expenses.\n";
        }
    }

    // Show all expenses
    void show() const {
        if (count == 0) {
            cout << "No expenses to show.\n";
            return;
        }

        cout << "Expenses:\n";
        for (int i = 0; i < count; ++i) {
            cout << list[i].name << " - ₹ " << list[i].cost << endl;
        }
    }

    // Show total cost of all expenses
    void total() const {
        double sum = 0;
        for (int i = 0; i < count; ++i) {
            sum += list[i].cost;
        }
        cout << "Total: ₹ " << sum << endl;
    }

private:
    static const int MAX = 100;   // Max expenses allowed
    Expense list[MAX];            // Array to store expenses
    int count;                    // Number of expenses added
};

int main() {
    Tracker tracker;
    char command;
    string name;
    double cost;

    cout<<"Welcome to the Tracker Application! \n";
    cout << "\nCommands given: a for (add), s for (show), t for (total), q for (quit)\n";

    while (true) {
        cout<<"\nPlease Enter your choice as given above : ";
        cin >> command;

        switch (command) {
            case 'a':
                cout << "\nPlease Enter the product's name: ";
                cin.ignore(); // Handle leftover newline
                getline(cin, name);
                cout << "Please Enter the product's cost: ";
                cin >> cost;
                tracker.add(name, cost);
                break;
            case 's':
                tracker.show();
                break;
            case 't':
                tracker.total();
                break;
            case 'q':
                cout << "Goodbye!, Have a Nice Day!\n";
                return 0;
            default:
                cout << "Invalid command.\n";
                break;
        }
    }

    return 0;
}

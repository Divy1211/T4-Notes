## Application Overview

Our MyCanteed@SUTD app is supposed to be able to:

### P0 Features:

1. Set up the information regarding the stalls in the canteen in a database.
2. Be able to show this information to our users. This way, users can plan when to visit the canteen (lets say a stall is closed/they don't have an item on the menu that they want etc.)
3. Users can indicate when they plan to visit a particular stall. Stall owners can prepare food accordingly (to help reduce waste)

### P1 Features:

1. Allow users to leave comments on a stall's page
2. Allow users to request certain food items

The app will consist of 3 main components:

### The User Interface

This will define certain activities. Some activities that we definitely will need to have are:

1. Log-In: Self explanatory, we should start the users out here. Move to Main Activity on login.
2. Main Activity: This is the activity that lets you see a list of all stalls and their status (open, closes at .../closed, opens at .../etc.)
3. Stall Info Activity: Once you click a stall's name in the main activity, it passes the info about which stall's information to display to this activity. This is the activity which will display all the information related to the stall. In this activity, an option should be given to the user to indicate if they will be eating at the stall at some point later (for the stall owners to be able to see)

This is not an exhaustive list, there may be more activities that we can add as per needed

The UI should define:

1. All of the actvities that the app needs to have
2. The layouts of each activity (the buttons, text views, image views, etc.) in the XML format (so all the different attributes like alignment and position on screen etc.)
3. The default values for all views etc.
4. A brief description of what each component in all the views does.
    1. For a text view, describe what text it will show.
    2. For an image view, describe the image that it needs to show.
    3. For a button, describe what it does when clicked.

### The Database

Using Firebase, we want to store the relevant information related to our users. A general outline of what will need to be done:

1. The specifics of how to set up and use a firebase instance needs to be looked into. Refer to the [Application Database Model](#application-database-model) section for details on what information our app will need to store. Do note that this is just tentative, and if we decide to add/remove certain features then relevant data can be added/removed as well. This ultimately depends on the UI design, and what info our app wishes to display to the users.
2. A class with relevant functions to get/post data need to be created (an API of sorts). These functions should be able to take in a parameter for the stall ID (and potentially other relevant parameters) whoes data needs to be retrieved/modified.
3. Data related to a stall can be retrieved by anyone, but some form of authorisation will be required to modfiy it (eg. anyone can view the menu, but only the actual stall owner should be able to edit!)


### The Backend

The backend is what will connect the user interface and the database of the app together and make it function in general. The outline of what needs to be done for this:

1. Use the specification from the UI design (in terms of the interaction behaviours of each component in all the activities) and implement that behaviour using action listeners and proper java code.
2. Using the functions given by the database API, retrieve and set the data in the relevant views to be displayed to the user.

### Documentation

The above process of coming up with the user interface, setting up firebase and creating the backend should be documented, showing why certain design choices were made. This is mainly useful for our report and maybe final presentation

## Current Task Delegations

Based on our previous discussions about the project, the following is the tentative task assignment

1. User Inferface: Eliana
2. Database: Ryan, Erick, Andre
3. Backend: Divy
4. Video: Zach, Ryan, Andre
5. Report: Divy, Zach, Wanglin
6. Poster: Eliana

## Application Database Model

This is a tentative data model for our app. (This is mostly the same as what we discussed last time in person)

### Enums

#### 1. StaffType
```java
enum StaffType {
    OTHER,
    HELPER,
    CHEF,
    OWNER,
}
```

#### 2. CustomerType
```java
enum CustomerType {
    FACULTY,
    OTHER,
}
```

#### 2. Day
```java
enum Day {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNUESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
}
```

### Classes

#### 1. User

```java
class User {
    private String username;
    private long userId;
    private String hash;

    public User(String username, String password, String confirmPassword);

    public String getUsername(String newUsername);
    public boolean setUsername(String newUsername);

    public long getUserId();

    public boolean checkHash(String password);
    public String getHash();
    public boolean setHash(String password);
}
```

#### 2. Customer
```java
class Customer extends User {
    private CustomerType type;
    private int breakfastTime; // 0-86399
    private int lunchTime; // 0-86399
    private int dinnerTime; // 0-86399
    private ArrayList<Day> eatDays;
    private boolean going;
    private int time; // 0-86399

    public CustomerType getType();
    public boolean setType(CustomerType type);

    public int getBreakfastTime();
    public boolean setBreakfastTime(int time);

    public int getLunchTime();
    public boolean setLunchTime(int time);

    public int getDinnerTime();
    public boolean setDinnerTime(int time);

    public ArrayList<Day> getEatDays();
    public boolean setEatDays(ArrayList<Day> eatDays);
}
```

#### 3. Staff
```java
class Staff extends User {
    private StaffType type;
    private int shiftStartTime; // 0-86399
    private int shiftEndTime; // 0-86399
    private boolean onBreak;
    private boolean onHoliday;

    public StaffType getType();
    public boolean setType(StaffType type);

    public int getShiftStartTime();
    public boolean setShiftStartTime(int time);

    public int getShiftEndTime();
    public boolean setShiftEndTime(int time);

    public boolean isOnBreak();
    public boolean setOnBreak(boolean onBreak);

    public boolean isOnHoliday();
    public boolean setOnHoliday(boolean onHoliday);

}
```

#### 4. Menu
```java
class MenuItem {
    private String name;
    private double price; // 0-86399
    private long stallId;

    public String getName();
    public boolean setName(String name);

    public double getPrice();
    public boolean setPrice(double price);
}
```

#### 5. Stall

```java
class Stall {
    private String name;
    private long stallId;
    private int openingTime;
    private int closingTime;
    private ArrayList<Staff> staffMembers;
    private ArrayList<MenuItem> menuItems;
    private boolean open;

    public String getName();
    public boolean setName(String name);

    public long getStallId();

    public int getOpeningTime();
    public boolean setOpeningTIme(int time);

    public int getClosingTime();
    public boolean setClosingTIme(int time);

    public ArrayList<Staff> getStaffMembers();
    public boolean setStaffMembers(ArrayList<Staff> staffMembers);

    public ArrayList<MenuItem> getMenuItems();

    public boolean isOpen();
    public boolean setOpen(boolean open);
}
```
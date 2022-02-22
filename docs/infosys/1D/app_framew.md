# Application Framework

## Enums

### 1. StaffType
```java
enum StaffType {
    OTHER,
    HELPER,
    CHEF,
    OWNER,
}
```

### 2. CustomerType
```java
enum CustomerType {
    FACULTY,
    OTHER,
}
```

### 2. Day
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

## Classes

### 1. User

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

### 2. Customer
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

### 3. Staff
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

### 4. Menu
```java
class MenuItem {
    private String name;
    private double price; // 0-86399

    public String getName();
    public boolean setName(String name);

    public double getPrice();
    public boolean setPrice(double price);
}
```

### 5. Stall

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

## To Do

1. Notifications
2. UI
3. Firebase
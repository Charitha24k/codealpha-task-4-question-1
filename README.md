import java.util.*;

public class Main {
    static Scanner scanner = new Scanner(System.in);
    static List<Room> rooms = new ArrayList<>();

    public static void main(String[] args) {
        initRooms();

        System.out.println("🏨 Welcome to Hotel Room Booking System");
        System.out.println("Type: search | book | cancel | view | help | exit");

        while (true) {
            System.out.print("\nEnter command: ");
            String command = scanner.nextLine().toLowerCase();

            switch (command) {
                case "search":
                    searchRooms();
                    break;
                case "book":
                    bookRoom();
                    break;
                case "cancel":
                    cancelBooking();
                    break;
                case "view":
                    viewBookings();
                    break;
                case "help":
                    printHelp();
                    break;
                case "exit":
                    System.out.println("Thank you! Visit again.");
                    return;
                default:
                    System.out.println("Invalid command. Type 'help' for options.");
            }
        }
    }

    static void initRooms() {
        rooms.add(new Room(101, "Single"));
        rooms.add(new Room(102, "Double"));
        rooms.add(new Room(103, "Suite"));
        rooms.add(new Room(104, "Single"));
        rooms.add(new Room(105, "Double"));
    }

    static void searchRooms() {
        System.out.print("Enter room type to search (Single/Double/Suite): ");
        String type = scanner.nextLine();

        System.out.println("Available " + type + " rooms:");
        for (Room r : rooms) {
            if (r.roomType.equalsIgnoreCase(type) && !r.isBooked) {
                System.out.println(" - Room " + r.roomNumber);
            }
        }
    }

    static void bookRoom() {
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.print("Enter room type to book (Single/Double/Suite): ");
        String type = scanner.nextLine();

        for (Room r : rooms) {
            if (r.roomType.equalsIgnoreCase(type) && !r.isBooked) {
                r.isBooked = true;
                r.guestName = name;
                System.out.println("✅ Room " + r.roomNumber + " booked successfully for " + name);
                return;
            }
        }

        System.out.println("❌ Sorry, no available rooms of type " + type);
    }

    static void cancelBooking() {
        System.out.print("Enter your name to cancel booking: ");
        String name = scanner.nextLine();

        for (Room r : rooms) {
            if (r.isBooked && r.guestName.equalsIgnoreCase(name)) {
                r.isBooked = false;
                r.guestName = "";
                System.out.println("✅ Booking canceled for " + name + " in Room " + r.roomNumber);
                return;
            }
        }

        System.out.println("❌ No booking found for " + name);
    }

    static void viewBookings() {
        System.out.println("📋 Current Bookings:");
        for (Room r : rooms) {
            System.out.println(" - " + r);
        }
    }

    static void printHelp() {
        System.out.println("Available Commands:");
        System.out.println(" - search : Search available rooms by type");
        System.out.println(" - book   : Book a room");
        System.out.println(" - cancel : Cancel a room booking");
        System.out.println(" - view   : View all bookings");
        System.out.println(" - help   : Show help menu");
        System.out.println(" - exit   : Exit the system");
    }
}

// Room class included below Main class
class Room {
    int roomNumber;
    String roomType;
    boolean isBooked;
    String guestName;

    Room(int roomNumber, String roomType) {
        this.roomNumber = roomNumber;
        this.roomType = roomType;
        this.isBooked = false;
        this.guestName = "";
    }

    public String toString() {
        return "Room " + roomNumber + " (" + roomType + ")" +
               (isBooked ? " - Booked by " + guestName : " - Available");
    }
}

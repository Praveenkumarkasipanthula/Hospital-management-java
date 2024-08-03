 import java.util.Scanner;

import javabasics.HospitalManagementSystem.Node;
class PatientRecord{
	int pId;
	String name;
	int age;
	String disease;
	String admitdate;
	String address;
	String phno;
	boolean isdischarged;
	public PatientRecord(int pId, String name, int age, String disease, String admitdate,String address, String phno) {
		super();
		this.pId = pId;
		this.name = name;
		this.age = age;
		this.disease = disease;
		this.admitdate = admitdate;
		this.address=address;
		this.phno = phno;
		this.isdischarged = false;
	}
	@Override
	public String toString() {
		return "PatientRecord [pId=" + pId + ", name=" + name + ", age=" + age + ", disease=" + disease + ", admitdate="
				+ admitdate +  ",address="+address+", phno=" + phno + ", isdischarged=" + (isdischarged ? "yes":"no")+ "]";
	}
}
class HospitalMangementSystems{
	class Node{
		PatientRecord data;
		Node next;
        public Node(PatientRecord data) {
            this.data = data;
            this.next = null;
        }
	}
	private Node head;

    public HospitalMangementSystems() {
        head = null;
    }
    public void addPatient(int patientId, String name, int age, String disease, String admittedDate, String address, String phoneNo) {
        PatientRecord newPatient = new PatientRecord(patientId, name, age, disease, admittedDate, address, phoneNo);
        Node newNode = new Node(newPatient);

        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
        System.out.println("Patient added successfully.");
    }
    public void dischargePatient(int patientId) {
        Node current = head;
        while (current != null) {
            if (current.data.patientId == patientId) {
                current.data.isDischarged = true;
                System.out.println("Patient discharged successfully.");
                return;
            }
            current = current.next;
        }
        System.out.println("Patient ID not found.");
    }
    public void getPatientInformation(int patientId) {
        Node current = head;
        while (current != null) {
            if (current.data.patientId == patientId) {
            	System.out.println("---------------------------");
                System.out.println("Patient ID: " + current.data.patientId);
                System.out.println("Name: " + current.data.name);
                System.out.println("Age: " + current.data.age);
                System.out.println("Disease: " + current.data.disease);
                System.out.println("Admitted Date: " + current.data.admittedDate);
                System.out.println("Address: " + current.data.address);
                System.out.println("Phone No: " + current.data.phoneNo);
                System.out.println("Discharged: " + (current.data.isDischarged ? "Yes" : "No"));
                System.out.println("---------------------------");
                
                return;
            }
            current = current.next;
        }
        System.out.println("Patient ID not found.");
    }
    public void displayAllPatients() {
        if (head == null) {
            System.out.println("No patients found.");
            return;
        }

        System.out.println("\n----------------------------------------------------------------------------------");
        System.out.println("| Patient ID |        Name          | Age |   Disease     | Admitted Date |        Address         |   Phone No   | Discharged |");
        System.out.println("----------------------------------------------------------------------------------");

        Node current = head;
        while (current != null) {
            System.out.println(current.data);
            current = current.next;
        }

        System.out.println("----------------------------------------------------------------------------------");
    }



}


public class Project {

	public static void main(String[] args) {
		 System.out.println("--------------------------------------------------------------------------------------");
         System.out.println("            *** Welcome to Hospital Management System Project in Java ***");
         System.out.println("--------------------------------------------------------------------------------------");
         Scanner scanner = new Scanner(System.in);
         HospitalManagementSystem hospital = new HospitalManagementSystem();
         
         while (true) {
        	 System.out.println("-----------------**********----------------");
             System.out.println("\n1. Add Patient\n2. Discharge Patient\n3. Get Patient Information\n4. Display All Patients\n5. Exit");
             System.out.print("Enter your choice: ");
             int choice = scanner.nextInt();
             scanner.nextLine();
             switch (choice) {
             case 1:
                 System.out.print("Enter Patient ID: ");
                 int patientId = scanner.nextInt();
                 scanner.nextLine(); // Consume the new line character left by nextInt()
                 System.out.print("Enter Name: ");
                 String name = scanner.nextLine();
                 System.out.print("Enter Age: ");
                 int age = scanner.nextInt();
                 scanner.nextLine(); // Consume the new line character left by nextInt()
                 System.out.print("Enter Disease: ");
                 String disease = scanner.nextLine();
                 System.out.print("Enter Admitted Date: ");
                 String admittedDate = scanner.nextLine();
                 System.out.print("Enter Address: ");
                 String address = scanner.nextLine();
                 System.out.print("Enter Phone No: ");
                 String phoneNo = scanner.nextLine();
                 hospital.addPatient(patientId, name, age, disease, admittedDate, address, phoneNo);
                 
                 
                 break;
             case 2:
            	 System.out.print("Enter Patient ID to discharge: ");
                 int dischargePatientId = scanner.nextInt();
                 hospital.dischargePatient(dischargePatientId);
                 break;
             case 3:
                 System.out.print("Enter Patient ID to get information: ");
                 int infoPatientId = scanner.nextInt();
                 hospital.getPatientInformation(infoPatientId);
                 break;
             case 4:
                 hospital.displayAllPatients();
                 break;
             case 5:
                 System.out.println("Exiting... Thank you!");
                 scanner.close();
                 System.exit(0);
             default:
                 System.out.println("Invalid choice. Please try again.");
             }
         }
	}

}


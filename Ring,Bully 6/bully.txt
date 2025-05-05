import java.io.*;
import java.util.Scanner;

public class leader_bully {
    static int n;
    static int pro[] = new int[10];
    static int sta[] = new int[10];
    static int co;

    public static void main(String args[]) throws IOException {
        System.out.println("-------------------------------------------------------");
        System.out.print("Enter the number of processes: ");
        Scanner in = new Scanner(System.in);
        n = in.nextInt();
        System.out.println("-------------------------------------------------------");

        for (int i = 0; i < n; i++) {
            System.out.println("** For process " + (i + 1) + ":");
            System.out.print("---> Status (1 for active, 0 for inactive): ");
            sta[i] = in.nextInt();
            System.out.print("---> Priority: ");
            pro[i] = in.nextInt();
            System.out.println("===============");
        }

        System.out.println("-------------------------------------------------------");
        System.out.print("*** Which process will initiate election? : ");
        int ele = in.nextInt();
        System.out.println("-------------------------------------------------------");
        elect(ele);
        System.out.println("*** Final coordinator is: " + co);
        System.out.println("-------------------------------------------------------");
    }

    static void elect(int ele) {
        ele = ele - 1;
        co = ele + 1;
        for (int i = 0; i < n; i++) {
            if (pro[ele] < pro[i]) {
                System.out.println("***** Election message is sent from " + (ele + 1) + " to " + (i + 1) + " *****");
                if (sta[i] == 1)
                    elect(i + 1);
            }
        }
    }
}

import java.io.*;
import java.util.Scanner;

public class leader_ring {
    static int n;
    static int pro[] = new int[100];
    static int sta[] = new int[100];
    static int prio[] = new int[100];
    static int co;

    public static void main(String args[]) throws IOException {
        System.out.println("----------------------------------------------------------");
        System.out.print("Enter the number of processes: ");
        Scanner in = new Scanner(System.in);
        n = in.nextInt();
        System.out.println("----------------------------------------------------------");

        for (int i = 0; i < n; i++) {
            System.out.println("** For process " + (i + 1) + " :");
            System.out.print("---> Status (1=active, 0=inactive): ");
            sta[i] = in.nextInt();
            System.out.print("---> Priority: ");
            pro[i] = in.nextInt();
            System.out.println("===============");
        }

        System.out.println("The ring formed is: ");
        for (int i = 1; i <= n; i++) {
            System.out.print(i + " -> ");
        }
        in.close();
        System.out.println("1");

        System.out.println("----------------------------------------------------------");
        System.out.print("Which process will initiate election? : ");
        int ele = in.nextInt();
        System.out.println("----------------------------------------------------------");

        elect(ele);
        System.out.println("Final coordinator is: " + co);
        System.out.println("----------------------------------------------------------");
    }

    static void elect(int ele) {
        int index = 0;
        int max = 0;

        // From the elected process to the end of the ring
        for (int i = (ele - 1); i < n; i++) {
            if (sta[i] == 1) {
                prio[index] = pro[i];
                index++;
            }
        }

        // From start of ring to just before the elected process
        for (int i = 0; i < (ele - 1); i++) {
            if (sta[i] == 1) {
                prio[index] = pro[i];
                index++;
            }
        }
        
        // Find maximum priority among active processes
        for (int i = 0; i < index; i++) {
            if (prio[i] > max) {
                max = prio[i];
            }
        }

        int ans =0 ;
        for (int i = 0; i < index; i++) {
            if (pro[i] == max) {
                ans = i+1;
            }
        }
        co = ans;


    }
}

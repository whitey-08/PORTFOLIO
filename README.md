import java.util.Scanner;

public class CongestionControl {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int cwnd = 1;
        int ssthresh = 8;

        System.out.print("Enter number of rounds: ");
        int rounds = sc.nextInt();

        System.out.println("\nRound\tCongestion Window\tPhase");

        for (int i = 1; i <= rounds; i++) {

            if (cwnd < ssthresh) {
                System.out.println(i + "\t" + cwnd +
                        "\t\t\tSlow Start");
                cwnd = cwnd * 2;
            }
            else {
                System.out.println(i + "\t" + cwnd +
                        "\t\t\tCongestion Avoidance");
                cwnd = cwnd + 1;
            }

            // Simulate packet loss at round 6
            if (i == 6) {
                System.out.println("Packet Loss Detected!");
                ssthresh = Math.max(cwnd / 2, 2);
                cwnd = 1;
                System.out.println("New Threshold: " + ssthresh);
            }
        }

        sc.close();
    }
}

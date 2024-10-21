package file_split;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class File_split {

    public static void main(String[] args) {
     Scanner scanner = new Scanner(System.in);
        Queue<String> queue = new LinkedList<>();
        
        // Step 1: Membaca file teks
        System.out.print("Masukkan path file teks: ");
        String filePath = scanner.nextLine();
        
        StringBuilder fileContent = new StringBuilder();
        
        try (BufferedReader br = new BufferedReader(new FileReader(new File(filePath)))) {
            String line;
            while ((line = br.readLine()) != null) {
                fileContent.append(line).append("\n");
            }
        } catch (IOException e) {
            System.out.println("Error membaca file: " + e.getMessage());
            return;
        }

        // Step 2: Memasukkan jumlah bagian yang diinginkan oleh pengguna
        System.out.print("Masukkan jumlah bagian yang ingin dipotong: ");
        int partCount = scanner.nextInt();
        scanner.nextLine(); // membersihkan input buffer
        
        String content = fileContent.toString();
        int contentLength = content.length();
        int partLength = contentLength / partCount;
        
        // Step 3: Memotong file dan menambahkan ke Queue
        for (int i = 0; i < partCount; i++) {
            int start = i * partLength;
            int end = (i == partCount - 1) ? contentLength : (i + 1) * partLength;
            String part = content.substring(start, end);
            queue.add(part);
        }

        // Step 4: Menampilkan potongan teks dalam Queue
        System.out.println("\nHasil potongan teks yang disimpan dalam Queue:");
        int partIndex = 1;
        while (!queue.isEmpty()) {
            System.out.println("Bagian " + partIndex + ":\n" + queue.poll());
            partIndex++;
        }

        scanner.close();
    }
}   

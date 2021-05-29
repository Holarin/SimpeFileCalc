import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Parser {
    int solve(String line) {
        if (line.contains("+")) {
            String[] strings = line.split("\\+");
            try {
                return Integer.parseInt(strings[0]) + Integer.parseInt(strings[1]);
            } catch (NumberFormatException e) {
                return 0;
            }
        }

        if (line.contains("-")) {
            String[] strings = line.split("-");
            try {
                return Integer.parseInt(strings[0]) - Integer.parseInt(strings[1]);
            } catch (NumberFormatException e) {
                return 0;
            }
        }

        if (line.contains("*")) {
            String[] strings = line.split("\\*");
            try {
                return Integer.parseInt(strings[0]) * Integer.parseInt(strings[1]);
            } catch (NumberFormatException e) {
                return 0;
            }
        }

        if (line.contains("/")) {
            String[] strings = line.split("/");
            try {
                return Integer.parseInt(strings[0]) / Integer.parseInt(strings[1]);
            } catch (NumberFormatException e) {
                return 0;
            }
        }

        return 0;
    }

    public List<Integer> loadFromFile(String data) {

        try {
            Parser parser = new Parser();
            List<Integer> integers = new ArrayList<>();
            File file = new File(data);
            FileReader fr = new FileReader(file);
            BufferedReader reader = new BufferedReader(fr);
            String line = reader.readLine();
            while (line != null) {
                integers.add(parser.solve(line));
                line = reader.readLine();
            }
            return integers;
        } catch (IOException e) {
            e.printStackTrace();
            return Collections.EMPTY_LIST;
        }
    }

    public void saveToFile(List<Integer> integers, String data) {

        FileWriter writer;
        try {
            writer = new FileWriter(data);
            for (Integer integer : integers) {
                writer.write(integer + System.getProperty("line.separator"));
            }
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        Parser parser = new Parser();
        parser.saveToFile(parser.loadFromFile("input.txt"), "output.txt");
    }
}

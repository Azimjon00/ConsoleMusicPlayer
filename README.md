import java.io.File;
import java.util.Scanner;

public class ConsoleMusicPlayer {

    private static String currentSong = null;
    private static boolean isPlaying = false;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Папка с песнями (можно менять)
        File folder = new File("C:\\Music");
        File[] files = folder.listFiles((dir, name) -> name.endsWith(".mp3"));

        if (files == null || files.length == 0) {
            System.out.println("Песен не найдено в папке " + folder.getAbsolutePath());
            return;
        }

        while (true) {
            System.out.println("\nМузыкальный плеер (только на Java)");
            System.out.println("Список песен:");
            for (int i = 0; i < files.length; i++) {
                System.out.println((i + 1) + ". " + files[i].getName());
            }
            System.out.println("0. Выйти");

            int choice = scanner.nextInt();
            scanner.nextLine(); // чтобы захватить Enter

            if (choice == 0) break;
            if (choice < 1 || choice > files.length) {
                System.out.println("Неверный выбор");
                continue;
            }

            currentSong = files[choice - 1].getName();
            isPlaying = true;
            System.out.println("Проигрывается: " + currentSong);

            while (isPlaying) {
                System.out.println("Введите команду: stop / pause / resume / next");
                String command = scanner.nextLine();

                switch (command.toLowerCase()) {
                    case "stop":
                        isPlaying = false;
                        System.out.println("Песня остановлена.");
                        break;
                    case "pause":
                        isPlaying = false;
                        System.out.println("Пауза...");
                        break;
                    case "resume":
                        isPlaying = true;
                        System.out.println("Возобновление: " + currentSong);
                        break;
                    case "next":
                        choice++;
                        if (choice > files.length) choice = 1;
                        currentSong = files[choice - 1].getName();
                        isPlaying = true;
                        System.out.println("Следующая песня: " + currentSong);
                        break;
                    default:
                        System.out.println("Неизвестная команда");
                }
            }
        }

        System.out.println("Выход из плеера");
        scanner.close();
    }
}

# 30 Segundos de Java

Inspirada en [30 seconds of code](https://github.com/Chalarangelo/30-seconds-of-code), esta es una colección de
fragmentos de código reutilizables, probados y compatibles con Java 17 que se pueden copiar y pegar en 30 segundos o
menos. Si está interesado en contribuir a esta biblioteca, consulte las [instrucciones](https://github.com/iluwatar/30-seconds-of-java/blob/master/CONTRIBUTE.md).

## Algoritmos

### Mergesort (Ordenamiento por mezcla)

```java
  public static void mergeSort(int arr[], int low, int high) {
    if (low >= high) {
        return;
    }
    int mid = (low + high) / 2;
    mergeSort(arr, low, mid);
    mergeSort(arr, mid + 1, high);
    merge(arr, low, high, mid);
}

private static void merge(int[] arr, int low, int high, int mid) {
    int temp[] = new int[(high - low + 1)];
    int i = low;
    int j = mid + 1;
    int k = 0;

    while (i <= mid && j <= high) {
        if (arr[i] < arr[j]) {
            temp[k++] = arr[i];
            i++;
        } else {
            temp[k++] = arr[j];
            j++;
        }
    }

    while (i <= mid) {
        temp[k++] = arr[i];
        i++;
    }

    while (j <= high) {
        temp[k++] = arr[j];
        j++;
    }

    for (int m = 0, n = low; m < temp.length; m++, n++) {
        arr[n] = temp[m];
    }
}
```

### Quicksort (Ordenamiento rápido)

```java
  public static void quickSort(int[] arr, int left, int right) {
    var pivotIndex = left + (right - left) / 2;
    var pivotValue = arr[pivotIndex];
    var i = left;
    var j = right;
    while (i <= j) {
        while (arr[i] < pivotValue) {
            i++;
        }
        while (arr[j] > pivotValue) {
            j--;
        }
        if (i <= j) {
            var tmp = arr[i];
            arr[i] = arr[j];
            arr[j] = tmp;
            i++;
            j--;
        }
        if (left < i) {
            quickSort(arr, left, j);
        }
        if (right > i) {
            quickSort(arr, i, right);
        }
    }
}
```

### Bubblesort (Ordenamiento de burbuja)

```java
  public static void bubbleSort(int[] arr) {
    var lastIndex = arr.length - 1;

    for (var j = 0; j < lastIndex; j++) {
        for (var i = 0; i < lastIndex - j; i++) {
            if (arr[i] > arr[i + 1]) {
                var tmp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = tmp;
            }
        }
    }
}
```

### Selectionsort (Ordenamiento por selección)

```java
  public static void selectionSort(int[] arr) {
    var len = arr.length;

    for (var i = 0; i < len - 1; i++) {
        var minIndex = i;

        for (var j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex])
                minIndex = j;
        }

        var tmp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = tmp;
    }
}
```

### InsertionSort (Ordenamiento por inserción)

```java
  public static void insertionSort(int[] arr) {
    for (var i = 1; i < arr.length; i++) {
        var tmp = arr[i];
        var j = i - 1;

        while (j >= 0 && arr[j] > tmp) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = tmp;
    }
}
```

### CountingSort (Ordenamiento por conteo)

```java
  public static void countingSort(int[] arr) {
    var max = Arrays.stream(arr).max().getAsInt();

    var count = new int[max + 1];

    for (var num : arr) {
        count[num]++;
    }

    for (var i = 1; i <= max; i++) {
        count[i] += count[i - 1];
    }

    var sorted = new int[arr.length];
    for (var i = arr.length - 1; i >= 0; i--) {
        var cur = arr[i];
        sorted[count[cur] - 1] = cur;
        count[cur]--;
    }

    var index = 0;
    for (var num : sorted) {
        arr[index++] = num;
    }
}
```

### CycleSort (Ordenamiento por ciclos)

```java
  public static int[] cycleSort(int[] arr) {
    int n = arr.length;
    int i = 0;
    while (i < n) {
        int correctpos = arr[i] - 1;
        if (arr[i] < n && arr[i] != arr[correctpos]) {
            int temp = arr[i];
            arr[i] = arr[correctpos];
            arr[correctpos] = temp;
        } else {
            i++;
        }
    }

    return arr;
}
```

### LinearSearch (Ordenamiento lineal)

```java
 public static int linearSearch(int[] arr, int item) {
    for (int i = 0; i < arr.length; i++) {
        if (item == arr[i]) {
            return i;
        }
    }
    return -1;
}
```

### LinearSearch in 2D Array (Ordenamiento lineal en matriz 2D)

```java
public static int[] linearSearch2dArray(int[][] arr, int target) {

    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr[i].length; j++) {
            if (arr[i][j] == target) {
                return new int[] {i, j};
            }
        }
    }

    return new int[] {-1, -1};
}
```

### BinarySearch (Ordenamiento binario)

```java
  public static int binarySearch(int[] arr, int left, int right, int item) {
    // La matriz arr[] debe estar ordenada
    if (right >= left) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == item) {
            return mid;
        }

        if (arr[mid] > item) {
            return binarySearch(arr, left, mid - 1, item);
        }

        return binarySearch(arr, mid + 1, right, item);
    }
    return -1;
}
```

### BinarySearch in 2D array (Ordenamiento binario en matriz 2D)

```java
public static int[] binarySearchIn2darr(int[][] matrix, int target) {
    int rows = matrix.length - 1;
    int cols = matrix[0].length - 1;

    if (rows == 1) {
        return binarySearch(matrix, target, 0, 0, cols);
    }

    int rstart = 0;
    int rend = rows;
    int cmid = cols / 2;

    while (rstart < rend - 1) {
        int rmid = rstart + (rend - rstart) / 2;
        if (matrix[rmid][cmid] > target) {
            rend = rmid;
        } else if (matrix[rmid][cmid] < target) {
            rstart = rmid;
        } else {
            return new int[] {rmid, cmid};
        }
    }
    if (matrix[rstart][cmid] == target) {
        return new int[] {rstart, cmid};
    }
    if (matrix[rend][cmid] == target) {
        return new int[] {rend, cmid};
    }
    if (target <= matrix[rstart][cmid - 1]) {
        return binarySearch(matrix, target, rstart, 0, cmid - 1);
    }
    if (target >= matrix[rstart][cmid + 1]) {
        return binarySearch(matrix, target, rstart, cmid + 1, cols);
    }
    if (target <= matrix[rend][cmid - 1]) {
        return binarySearch(matrix, target, rend, 0, cmid - 1);
    }
    if (target <= matrix[rend][cmid + 1]) {
        return binarySearch(matrix, target, rend, cmid + 1, cols);
    }
    return new int[] {-1, -1};
}

static int[] binarySearch(int[][] matrix, int target, int row, int cstart, int cend) {
    while (cstart <= cend) {
        int cmid = cstart + (cend - cstart) / 2;
        if (matrix[row][cmid] > target) {
            cend = cmid - 1;
        } else if (matrix[row][cmid] < target) {
            cstart = cend + 1;
        } else {
            return new int[] {row, cmid};
        }
    }
    return new int[] {-1, -1};
}
```

### SieveOfEratosthenes (Criba de Eratóstenes)

```java
  public static boolean[] sieveOfEratosthenes(int n) {
    boolean[] isPrime = new boolean[n + 1];
    for (int i = 0; i < isPrime.length; i++) {
        isPrime[i] = true;
    }

    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i] == true) {
            for (int j = i * i; j <= n; j += i) {
                isPrime[j] = false;
            }
        }
    }

    return isPrime;
}
```

## Arreglos

### Concatenación de arreglos

```java
  public static <T> T[] arrayConcat(T[] first, T[] second) {
    var result = Arrays.copyOf(first, first.length + second.length);
    System.arraycopy(second, 0, result, first.length, second.length);
    return result;
}
```

### Concatenación de n arreglos

```java
  public static <T> T[] nArrayConcat(T[] first, T[]... rest) {
    var totalLength = first.length;
    for (var array : rest) {
        totalLength += array.length;
    }
    var result = Arrays.copyOf(first, totalLength);
    var offset = first.length;
    for (var array : rest) {
        System.arraycopy(array, 0, result, offset, array.length);
        offset += array.length;
    }
    return result;
}
```

### Contar ocurrencias de un elemento en un arreglo

```java
  public static <T> boolean allEqual(T[] arr) {
    return Arrays.stream(arr).distinct().count() == 1;
}
```

### Hallar la media de una matriz de enteros

```java
  public static double arrayMean(int[] arr) {
    return (double) Arrays.stream(arr).sum() / arr.length;
}
```

### Hallar la mediana de una matriz de enteros

```java
  public static double arrayMedian(int[] arr) {
    Arrays.sort(arr);
    var mid = arr.length / 2;
    return arr.length % 2 != 0 ? (double) arr[mid] : (double) (arr[mid] + arr[mid - 1]) / 2;
}
```

### Buscar el modo de una matriz de enteros

```java
public static int modeArray(int[] arr) {
    int mode = 0;
    int maxcount = 0;

    for (int i = 0; i < arr.length; i++) {
        int count = 0;

        for (int j = 0; j < arr.length; j++) {
            if (arr[i] == arr[j]) {
                count++;
            }
        }
        if (count > maxcount) {
            maxcount = count;
            mode = arr[i];
        }
    }
    return mode;
}
```

### Hallar la suma de una matriz de enteros

```java
  public static int arraySum(int[] arr) {
    return Arrays.stream(arr).sum();
}
```

### Encontrar el número entero máximo de la matriz

```java
  public static int findMax(int[] arr) {
    return Arrays.stream(arr).reduce(Integer.MIN_VALUE, Integer::max);
}
```

### Encontrar el número entero mínimo de la matriz

```java
  public static int findMin(int[] arr) {
    return Arrays.stream(arr).reduce(Integer.MAX_VALUE, Integer::min);
}
```

### Matriz inversa

```java
  public static <T> T[] reverseArray(T[] array, int start, int end) {
    if (start > end || array == null) {
        throw new IllegalArgumentException("Invalid argument!");
    }
    int minimumSizeArrayForReversal = 2;
    if (start == end || array.length < minimumSizeArrayForReversal) {
        return array;
    }
    while (start < end) {
        T temp = array[start];
        array[start] = array[end];
        array[end] = temp;
        start++;
        end--;
    }
    return array;
}
```

## Codificación

### Cadena codificada en Base64

```java
  public static String encodeBase64(String input) {
    return Base64.getEncoder().encodeToString(input.getBytes());
}
```

### Cadena decodificada en Base64

```java
  public static String decodeBase64(String input) {
    return new String(Base64.getDecoder().decode(input.getBytes()));
}
```

## Archivos

### Listar directorios

```java
  public static File[] listDirectories(String path) {
    return new File(path).listFiles(File::isDirectory);
}
```

### Listar archivos en el directorio

```java
  public static File[] listFilesInDirectory(final File folder) {
    return folder.listFiles(File::isFile);
}
```

### Listar archivos en el directorio de forma recursiva

```java
  public static List<File> listAllFiles(String path) {
    var all = new ArrayList<File>();
    var list = new File(path).listFiles();

    if (list != null) {  // En caso de error de acceso, la lista es nula
        for (var f : list) {
            if (f.isDirectory()) {
                all.addAll(listAllFiles(f.getAbsolutePath()));
            } else {
                all.add(f.getAbsoluteFile());
            }
        }
    }
    return all;
}
```

### Lectura de líneas de un archivo a una lista de cadenas

```java
  public static List<String> readLines(String filename) throws IOException {
    return Files.readAllLines(new File(filename).toPath());
}
```

### Comprimir archivos

```java
  public static void zipFile(String srcFilename, String zipFilename) throws IOException {
    var srcFile = new File(srcFilename);
    try (var fileOut = new FileOutputStream(zipFilename);
         var zipOut = new ZipOutputStream(fileOut);
         var fileIn = new FileInputStream(srcFile);) {
        var zipEntry = new ZipEntry(srcFile.getName());
        zipOut.putNextEntry(zipEntry);
        final var bytes = new byte[1024];
        int length;
        while ((length = fileIn.read(bytes)) >= 0) {
            zipOut.write(bytes, 0, length);
        }
    }
}
```

### Comprimir multiples archivos

```java
  public static void zipFiles(String[] srcFilenames, String zipFilename) throws IOException {
    try (var fileOut = new FileOutputStream(zipFilename);
         var zipOut = new ZipOutputStream(fileOut);) {
        for (var i = 0; i < srcFilenames.length; i++) {
            var srcFile = new File(srcFilenames[i]);
            try (var fileIn = new FileInputStream(srcFile)) {
                var zipEntry = new ZipEntry(srcFile.getName());
                zipOut.putNextEntry(zipEntry);
                final var bytes = new byte[1024];
                int length;
                while ((length = fileIn.read(bytes)) >= 0) {
                    zipOut.write(bytes, 0, length);
                }
            }
        }
    }
}
```

### Comprime un directorio

```java
  public static void zipDirectory(String srcDirectoryName, String zipFileName) throws IOException {
    var srcDirectory = new File(srcDirectoryName);
    try (var fileOut = new FileOutputStream(zipFileName);
         var zipOut = new ZipOutputStream(fileOut)) {
        zipFile(srcDirectory, srcDirectory.getName(), zipOut);
    }
}

public static void zipFile(File fileToZip, String fileName, ZipOutputStream zipOut) throws IOException {
    if (fileToZip.isHidden()) { // Ignorar archivos ocultos como estándar
        return;
    }
    if (fileToZip.isDirectory()) {
        if (fileName.endsWith("/")) {
            zipOut.putNextEntry(new ZipEntry(fileName)); // Para comprimir a continuación
            zipOut.closeEntry();
        } else {
            // Añada la marca "/" explícitamente para preservar la estructura mientras se realiza la acción de descomprimir.
            zipOut.putNextEntry(new ZipEntry(fileName + "/"));
            zipOut.closeEntry();
        }
        var children = fileToZip.listFiles();
        for (var childFile : children) { //Aplicar recursivamente la función a todos los hijos
            zipFile(childFile, fileName + "/" + childFile.getName(), zipOut);
        }
        return;
    }
    try (var fis = new FileInputStream(fileToZip)
         // Comenzar a comprimir una vez que sabemos que es un archivo
    ) {
        var zipEntry = new ZipEntry(fileName);
        zipOut.putNextEntry(zipEntry);
        var bytes = new byte[1024];
        var length = 0;
        while ((length = fis.read(bytes)) >= 0) {
            zipOut.write(bytes, 0, length);
        }
    }
}
```

## Matemáticas

### EvenOrOdd (Par o impar)

```java
public static String evenodd(int num) {
    if (num % 2 == 0) {
        return "even";
    } else {
        return "odd";
    }
}
```

### Raíz cuadrada de un número

```java
public static double sqrt(int num, int p) {
    int start = 0;
    int end = num;
    double root = 0.0;

    while (start <= end) {
        int mid = start + (end - start) / 2;

        if ((mid * mid) > num) {
            end = mid - 1;
        } else if ((mid * mid) < num) {
            start = mid + 1;
        } else {
            return mid;
        }
    }
    double incr = 0.1;
    for (int i = 0; i < p; i++) {
        while (root * root < num) {
            root = root + incr;
        }
        root = root - incr;
        incr = incr / 10;
    }
    return root;
}
```

### Fibonacci

```java
  public static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

### Fibonacci interactivo

```java
  public static int iterativeFibonacci(int number) {
    List<Integer> list = new ArrayList<>();
    list.add(0);
    list.add(1);
    for (int i = 2; i < number + 1; i++) {
        list.add(list.get(i - 2) + list.get(i - 1));
    }
    return list.get(number);
}
```

### Factorial

```java
  public static int factorial(int number) {
    var result = 1;
    for (var factor = 2; factor <= number; factor++) {
        result *= factor;
    }
    return result;
}
```

### Factorial recursivo

```java
  public static int recursiveFactorial(int number) {
    var initial = 0;
    if (number == initial) {
        return initial + 1;
    }
    return number * recursiveFactorial(number - 1);
}
```

### Fórmula Haversine

```java
  // Radio de la esfera en la que se encuentran los puntos, en este caso la Tierra.
private static final double SPHERE_RADIUS_IN_KM = 6372.8;

public static double findHaversineDistance(double latA, double longA, double latB, double longB) {
    if (!isValidLatitude(latA) || !isValidLatitude(latB) || !isValidLongitude(longA) || !isValidLongitude(longB)) {
        throw new IllegalArgumentException();
    }

    // Calcular las diferencias de latitud y longitud
    var latitudeDiff = Math.toRadians(latB - latA);
    var longitudeDiff = Math.toRadians(longB - longA);

    var latitudeA = Math.toRadians(latA);
    var latitudeB = Math.toRadians(latB);

    // Cálculo de la distancia según la fórmula haversine
    var a = Math.pow(Math.sin(latitudeDiff / 2), 2) + Math.pow(Math.sin(longitudeDiff / 2), 2) * Math.cos(
            latitudeA) * Math.cos(latitudeB);
    var c = 2 * Math.asin(Math.sqrt(a));
    return SPHERE_RADIUS_IN_KM * c;
}

// Comprobar si el valor de la latitud es válido
private static boolean isValidLatitude(double latitude) {
    return latitude >= -90 && latitude <= 90;
}

// Comprobación de un valor de longitud válido
private static boolean isValidLongitude(double longitude) {
    return longitude >= -180 && longitude <= 180;
}
```

### Lotería

```java
  public static Integer[] performLottery(int numNumbers, int numbersToPick) {
    var numbers = new ArrayList<Integer>();
    for (var i = 0; i < numNumbers; i++) {
        numbers.add(i + 1);
    }

    Collections.shuffle(numbers);
    return numbers.subList(0, numbersToPick).toArray(new Integer[numbersToPick]);
}
```

### Algoritmo Luhn

```java
public static int calculateLuhnChecksum(long num) {
    if (num < 0) {
        throw new IllegalArgumentException("Non-negative numbers only.");
    }
    final var numStr = String.valueOf(num);

    var sum = 0;
    var isOddPosition = true;
    // Hacemos un bucle sobre los dígitos de numStr de derecha a izquierda.
    for (var i = numStr.length() - 1; i >= 0; i--) {
        final var digit = Integer.parseInt(Character.toString(numStr.charAt(i)));
        final var substituteDigit = (isOddPosition ? 2 : 1) * digit;

        final var tensPlaceDigit = substituteDigit / 10;
        final var onesPlaceDigit = substituteDigit % 10;
        sum += tensPlaceDigit + onesPlaceDigit;

        isOddPosition = !isOddPosition;
    }
    final var checksumDigit = (10 - (sum % 10)) % 10;
    // El módulo exterior maneja el caso de borde `num = 0`.
    return checksumDigit;
}
```

### Máximo común divisor

```java
  public static int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}
```

### Mínimo común múltiplo

```java
  public static int lcm(int a, int b) {
    int max = a > b ? a : b;
    int min = a < b ? a : b;
    for (int i = 1; i <= min; i += 1) {
        int prod = max * i;
        if (prod % min == 0) {
            return prod;
        }
    }
    return max * min;
}
```

### Prime

```java
  public static boolean isPrime(int number) {
    if (number < 3) {
        return true;
    }

    // comprobar si n es múltiplo de 2
    if (number % 2 == 0) {
        return false;
    }

    // si no, entonces solo comprueba las probabilidades
    for (var i = 3; i * i <= number; i += 2) {
        if (number % i == 0) {
            return false;
        }
    }
    return true;
}
```

### Conversión binaria de números naturales

```java
  public static String toBinary(long naturalNumber) {
    if (naturalNumber < 0) {
        throw new NumberFormatException("Negative Integer, this snippet only accepts " + "positive integers");
    }
    if (naturalNumber == 0) {
        return "0";
    }
    final Stack<Long> binaryBits = Stream.iterate(naturalNumber, n -> n > 0, n -> n / 2)
            .map(n -> n % 2)
            .collect(Stack::new, Stack::push, Stack::addAll);
    return Stream.generate(binaryBits::pop).limit(binaryBits.size()).map(String::valueOf).collect(Collectors.joining());
}

public static Long fromBinary(String binary) {
    binary.chars().filter(c -> c != '0' && c != '1').findFirst().ifPresent(in -> {
        throw new NumberFormatException("Binary string contains values other than '0' and '1'");
    });
    return IntStream.range(0, binary.length())
            .filter(in -> binary.charAt(binary.length() - 1 - in) == '1')
            .mapToLong(in -> ((long) 0b1) << in)
            .sum();
}

```

### Clasificación Elo

```java

final static int BASE = 400;
final static int RATING_ADJUSTMENT_FACTOR = 32;

public static double calculateMatchRating(double firstPlayerRating, double secondPlayerRating, double result) {
    double ratingDiff = ((secondPlayerRating - firstPlayerRating) * 1.0) / BASE;
    double logisticDiff = Math.pow(10, ratingDiff);
    double firstPlayerExpectedScore = 1.0 / (1 + logisticDiff);
    double firstPlayerActualScore = result;
    double newRating = firstPlayerRating + RATING_ADJUSTMENT_FACTOR * (firstPlayerActualScore - firstPlayerExpectedScore);
    return newRating;
}
```

## Media

### Capturar pantalla

```java
  public static void captureScreen(String filename) throws AWTException, IOException {
    var screenSize = Toolkit.getDefaultToolkit().getScreenSize();
    var screenRectangle = new Rectangle(screenSize);
    var robot = new Robot();
    var image = robot.createScreenCapture(screenRectangle);
    ImageIO.write(image, "png", new File(filename));
}
```

## Redes

### HTTP GET

```java
  public static HttpResponse<String> httpGet(String uri) throws Exception {
    var client = HttpClient.newHttpClient();
    var request = HttpRequest.newBuilder().uri(URI.create(uri)).build();
    return client.send(request, BodyHandlers.ofString());
}
```

### HTTP POST

```java
  public static HttpResponse<String> httpPost(String address, HashMap<String, String> arguments) throws IOException,
        InterruptedException {
    var sj = new StringJoiner("&");
    for (var entry : arguments.entrySet()) {
        sj.add(URLEncoder.encode(entry.getKey(), "UTF-8") + "=" + URLEncoder.encode(entry.getValue(), "UTF-8"));
    }

    var out = sj.toString().getBytes(StandardCharsets.UTF_8);
    var request = HttpRequest.newBuilder()
            .uri(URI.create(address))
            .headers("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8")
            .POST(BodyPublishers.ofByteArray(out))
            .build();

    return HttpClient.newHttpClient().send(request, BodyHandlers.ofString());
}
```

## Cadenas

### Comprobación de palíndromos

```java
  public static boolean isPalindrome(String s) {
    for (int i = 0, j = s.length() - 1; i < j; i++, j--) {
        while (i < j && !Character.isLetter(s.charAt(i))) {
            i++;
        }
        while (i < j && !Character.isLetter(s.charAt(j))) {
            j--;
        }

        if (Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) {
            return false;
        }
    }

    return true;
}
```

### Cadena inversa

```java
  public static String reverseString(String s) {
    return new StringBuilder(s).reverse().toString();
}
```

### Cadena a fecha

```java
  public static Date stringToDate(String date, String format) throws ParseException {
    var simpleDateFormat = new SimpleDateFormat(format);
    return simpleDateFormat.parse(date);
}
```

### Comprobación de anagramas

```java
  public boolean isAnagram(String s1, String s2) {
    var l1 = s1.length();
    var l2 = s2.length();
    var arr1 = new int[256];
    var arr2 = new int[256];
    if (l1 != l2) {
        return false;
    }

    for (var i = 0; i < l1; i++) {
        arr1[s1.charAt(i)]++;
        arr2[s2.charAt(i)]++;
    }

    return Arrays.equals(arr1, arr2);
}
```

### Encontrar la distancia Levenshtein

```java
  public static int findLevenshteinDistance(String word1, String word2) {
    // Si word2 está vacía, se elimina
    int[][] ans = new int[word1.length() + 1][word2.length() + 1];
    for (int i = 0; i <= word1.length(); i++) {
        ans[i][0] = i;
    }

    // si word1 está vacía, añadir
    for (int i = 0; i <= word2.length(); i++) {
        ans[0][i] = i;
    }

    // Ninguno está vacío
    for (int i = 1; i <= word1.length(); i++) {
        for (int j = 1; j <= word2.length(); j++) {
            int min = Math.min(Math.min(ans[i][j - 1], ans[i - 1][j]), ans[i - 1][j - 1]);
            ans[i][j] = word1.charAt(i - 1) == word2.charAt(j - 1) ? ans[i - 1][j - 1] : min + 1;
        }
    }
    return ans[word1.length()][word2.length()];
}
```

### Comparar versión

```java
  public static int compareVersion(String v1, String v2) {
    Function<String, String[]> getVersionComponents = version -> version.replaceAll(".*?((?<!\\w)\\d+([.-]\\d+)*).*",
            "$1", "$1").split("\\.");

    var components1 = getVersionComponents.apply(v1);
    var components2 = getVersionComponents.apply(v2);
    int length = Math.max(components1.length, components2.length);

    for (int i = 0; i < length; i++) {
        Integer c1 = i < components1.length ? Integer.parseInt(components1[i]) : 0;
        Integer c2 = i < components2.length ? Integer.parseInt(components2[i]) : 0;
        int result = c1.compareTo(c2);
        if (result != 0) {
            return result;
        }
    }
    return 0;
}
```

### Obtener letras comunes

```java
  public static String getCommonLetters(String firstStr, String secondStr) {
    Set<String> commonLetters = new HashSet<>();
    for (Character currentCharacter : firstStr.toCharArray()) {
        if (isCommonLetter(secondStr, currentCharacter)) {
            commonLetters.add(currentCharacter.toString());
        }
    }
    return String.join(" ", commonLetters);
}

private static boolean isCommonLetter(String str, Character character) {
    return str.contains(character.toString()) && Character.isLetter(character);
}
```

### Recuento máximo de un carácter

```java
 public static int getMaxCharacterCount(String str, char character) {
    int characterCount = 0;
    int maxCharacterCount = 0;
    for (int i = 0; i < str.length(); i++) {
        if ((str.charAt(i)) == character) {
            characterCount++;
            maxCharacterCount = Math.max(maxCharacterCount, characterCount);
        } else {
            characterCount = 0;
        }
    }
    return maxCharacterCount;
}
```

### Eliminar caracteres duplicados de una cadena

```java
  public static String removeDuplicateCharacters(String str) {
    char[] charsOfStr = str.toCharArray();
    Set<String> uniqueCharacters = new HashSet<>();
    for (char character : charsOfStr) {
        uniqueCharacters.add(String.valueOf(character));
    }
    return String.join("", uniqueCharacters);
}
```

## Clases

### Obtener el nombre de los métodos

```java
  public static List<String> getAllMethods(final Class<?> cls) {
    return Arrays.stream(cls.getDeclaredMethods()).map(Method::getName).collect(Collectors.toList());
}
```

### Obtener nombres de campos públicos

```java
  public static List<String> getAllFieldNames(final Class<?> cls) {
    return Arrays.stream(cls.getFields()).map(Field::getName).collect(Collectors.toList());
}
```

### Obtener todos los nombres de campo

```java
  public static List<String> getAllFieldNames(final Class<?> cls) {
    var fields = new ArrayList<String>();
    var currentCls = cls;
    while (currentCls != null) {
        fields.addAll(Arrays.stream(currentCls.getDeclaredFields())
                .filter(field -> !field.isSynthetic())
                .map(Field::getName)
                .collect(Collectors.toList()));
        currentCls = currentCls.getSuperclass();
    }
    return fields;
}
```

### Crear objeto

```java
  public static Object createObject(String cls) throws NoSuchMethodException, IllegalAccessException,
        InvocationTargetException, InstantiationException, ClassNotFoundException {
    var objectClass = Class.forName(cls);
    var objectConstructor = objectClass.getConstructor();
    return objectConstructor.newInstance();
}
```

## Entrada/Salida

### Leer archivo por flujo

```java
  public static List<String> readFile(String fileName) throws FileNotFoundException {
    try (Stream<String> stream = new BufferedReader(new FileReader(fileName)).lines()) {
        return stream.collect(Collectors.toList());
    }
}
```

### InputStream a String

```java
  public static String inputStreamToString(InputStream inputStream) throws IOException {
    try (var reader = new BufferedReader(new InputStreamReader(inputStream))) {
        var stringBuilder = new StringBuilder();
        var data = reader.read();

        while (data != -1) {
            stringBuilder.append((char) data);
            data = reader.read();
        }
        return stringBuilder.toString();
    }
}
```

## Hilos

### Crear pool de hilos

```java
  public static ExecutorService createFixedThreadPool() {
    return Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());
}
```

## Fecha

### Añadir nº de días hasta la fecha

```java
  public static Date addDaysToDate(Date date, int noOfDays) {
    if (date != null) {
        Calendar cal = Calendar.getInstance();
        cal.setTime(date);
        cal.add(Calendar.DAY_OF_MONTH, noOfDays);
        return cal.getTime();
    }
    return null;
}
```

### Añadir días a la fecha local

```java
 public static LocalDate addDaysToLocalDate(LocalDate date, long noOfDays) {
    return date != null ? date.plusDays(noOfDays) : null;
}
```

### Cálculo de la diferencia entre dos fechas

```java
 public static long getYearsDifference(LocalDate firstTime, LocalDate secondTime) {
    var yearsDifference = ChronoUnit.YEARS.between(firstTime, secondTime);
    return Math.abs(yearsDifference);
}
```

```java
 public static long getMonthsDifference(LocalDate firstTime, LocalDate secondTime) {
    var monthsDifference = ChronoUnit.MONTHS.between(firstTime, secondTime);
    return Math.abs(monthsDifference);
}
```

```java
 public static long getDaysDifference(LocalDate firstTime, LocalDate secondTime) {
    var daysDifference = ChronoUnit.DAYS.between(firstTime, secondTime);
    return Math.abs(daysDifference);
}
```

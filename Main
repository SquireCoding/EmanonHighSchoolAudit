import java.io.*;
import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Scanner;
public class Main  {
    public static boolean turbo = false; //simply, this determines if
    public static final String RED = "\u001B[31m";
    public static final String GREEN = "\u001B[32m";
    public static final String YELLOW = "\u001B[33m";
    public static final String BLUE = "\u001B[34m";
    public static final int YEAR_STYLE = 2024;
    static LocalDateTime ti = LocalDateTime.now();
    static String nu = "src/Outputs/OutputAtRuntime" + ti.getMonthValue()+"-"+ti.getDayOfMonth()+"-" + ti.getYear() + " (" + ti.getHour()+ ";" + ti.getMinute() + ";" + ti.getSecond() + ")";
    public static void main(String[] args) {
        if (YEAR_STYLE==2023) {
            run2023mode();
        }
        if (YEAR_STYLE==2024) {
            run2024mode();
        }
    }
    public static int distFiles(File f) {
        Scanner s = null;
        try {
            s = new Scanner(f);
        } catch (FileNotFoundException e) {
            throw new RuntimeException(e);
        }
        while (s.hasNextLine()) {
            if (s.nextLine().contains("*")) return 2023;
        }
        return 2024;
    }

    public static void run2024mode() {
        turbo = false;
        try {
            File folda = new File("src/GraduationCSVFiles");
            folda.mkdir();
            File[] matchingFiles = folda.listFiles((dir, name) -> name.endsWith(".csv"));
            new File("src/Outputs").mkdir();
            System.out.println(nu);
            File tem1p = new File(nu);
            System.out.println(tem1p.getAbsolutePath());
            new File(nu).mkdir();
            File curr = new File(nu+"/DetailedDocument.txt");
            curr.createNewFile();
            Scanner in = new Scanner(System.in);
            clear();
            System.out.println(YELLOW + "Hello, and welcome to the Formatting and Outputting program, created by KATZ Studios \nfor Emanon High School/North Cambria District High School. You are currently in "+ YEAR_STYLE+" mode.\nTo input a file, put it into the \"GraduationCSVFiles\"  Folder, and then select it here. Here are your files:\n");
            assert matchingFiles != null;
            for (File fop: matchingFiles) {
                System.out.println(GREEN + fop.getName()+ BLUE+" [Most likely edition: "+distFiles(fop)+"]");
            }
            if (matchingFiles.length==0) {
                System.out.println(RED + "It appears you do not have any files ready to use. Please move some .csv files into the \"GraduationCSVFiles\"  Folder, and then try again.");
                System.exit(0);
            }
            System.out.println(YELLOW + "\nPlease enter the file name you wish to use, adding a TUR to the front to use turbo mode." + BLUE);
            String inp;
            File f;
            inp  = in.next();
            if (inp.startsWith("TUR")) {
                turbo = true;
                StringBuilder sb = new StringBuilder(inp);
                sb.delete(0,3);
                inp = sb.toString();
            }
            if (!inp.contains(".csv")) {
                inp+=".csv";
            }
            if (inp.equalsIgnoreCase("s.csv")) {
                inp = "SampleReport.csv";
            }
            f = new File("src/GraduationCSVFiles/" + inp);
            BufferedReader reader = new BufferedReader(new FileReader("src/GraduationCSVFiles/" + inp));
            int lines = -1;
            while (reader.readLine() != null) lines++;
            reader.close();
            int current = 1;
            Scanner s = new Scanner(f);
            s.nextLine();
            ArrayList<Student> honorStud = new ArrayList<>();
            ArrayList<Student> passStud = new ArrayList<>();
            ArrayList<Student> failStud = new ArrayList<>();
            String start = "<html> <head> <title> Emanon High School Graduation Audit </title><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\"> <style> body {background-color:#ffffff;background-image:url(https://lh6.googleusercontent.com/xAd15-3Sp-PXZpxeyUvtYQVgZEZOqZFrTaoLCJYftNc-gbixdwvgt0fmGpcdshwEuQZsiZwxiF82RfD_RbEXblA=w16383);background-repeat:no-repeat;background-position:center left;background-attachment:fixed;} h1{font-family:Arial, sans-serif;letter-spacing:10px;color:#f2c645;background-color:#000000;} p {font-family:Georgia, serif;font-size:14px;font-style:normal;font-weight:normal;color:#ffffff;background-color:#000000;} </style> </head> <body> <h1>EHS GRADUATION PAPER</h1> <p>Kids who graduated with honors: ";
            if (turbo) {
                clear();
                System.out.println(RED + "Turbo mode enabled.");
            }
            while (s.hasNextLine()) {
                if (!turbo) {
                    clear();
                    System.out.println(YELLOW + "Working on student " + current + " of " + lines + "...");
                    current++;
                }
                String line = s.nextLine();
                line = line.replace(","," ,");
                line = line.replace("+","");
                line = line.replace("-","");
                String[] data = line.split(",");
                Student javon = new Student(data[1].replace(" ",""), data[0].replace(" ",""));
                DiagnosticFile.writeln("\n\nStudent Name: " + javon.getName());
                for (int j = 2; j<data.length; j++) {
                    data[j]=data[j].replace(" ","");
                    Grade g = new Grade(data[j]);
                    if (j<9) {
                        g.clas=C.SOCIALSTUDIES;
                        if (j==6||j==7) {
                            g.specClass="AH";
                        }
                        if (j==8) {
                            g.specClass="AG";
                        }
                    }
                    if (j>8&&j<15) {
                        g.clas=C.MATH;
                        if (j==11||j==12) {
                            g.specClass="GE";
                        }
                    }
                    if (j>14&&j<21) {
                        g.clas=C.SCIENCE;
                        if (j==17||j==18) {
                            g.specClass="LS";
                        }
                    }
                    if (j>20&&j<29) {
                        g.clas=C.ENGLISH;
                    }
                    if (j>28&&j<31) {
                        g.specClass="PE";
                    }
                    if (j==31) {
                        g.specClass="S";
                    }
                    if (j>31&&j<34) {
                        g.specClass="FA";
                    }
                    if (j==34) {
                        g.specClass="CO";
                    }
                    if (g.clas==null) g.clas = C.ELECTIVE;
                    javon.add(g);
                }
                GraduationStatus gr = canGraduate2024(javon);
                if (gr==GraduationStatus.HONORS) {
                    honorStud.add(javon);
                }
                if (gr==GraduationStatus.FAIL) {
                    failStud.add(javon);
                }
            }
            Student[] failers = new Student[failStud.size()];
            failers = failStud.toArray(failers);
            clear();
            System.out.println("Sorting failed students...");
            Arrays.sort(failers, Collections.reverseOrder());
            Student[] passers = new Student[passStud.size()];
            passers = passStud.toArray(passers);
            clear();
            System.out.println("Sorting passed students...");
            Arrays.sort(passers, Collections.reverseOrder());
            Student[] honorers = new Student[honorStud.size()];
            honorers = honorStud.toArray(honorers);
            clear();
            System.out.println("Sorting honors students...");
            Arrays.sort(honorers, Collections.reverseOrder());
            StringBuilder allHonorGrad = new StringBuilder();
            clear();
            System.out.println("Creating HTML File...");
            for (int ii = 0; (ii<honorers.length&&ii<20); ii++) {
                String en = ", ";
                if (ii==(honorers.length-1)) en = "";
                allHonorGrad.append(honorers[ii].getName()).append(en);
            }
            start+=allHonorGrad+ "</p> <p></p> <p>Kids who did not graduate: ";
            StringBuilder allHonorGradll= new StringBuilder();
            for (int ii = 0; ii<failers.length; ii++) {
                String en = ", ";
                if (ii==(failers.length-1)) en = "";
                allHonorGradll.append(failers[ii].getName()).append(en);
            }
            start+=allHonorGradll+"</p> </body> </html>";
            String fileName = nu+"//Output.html";
            File fi = new File(fileName);
            fi.createNewFile();
            FileWriter fid = new FileWriter(fileName);
            clear();
            System.out.println("Outputting HTML File...");
            fid.write(start);
            fid.close();
            clear();
            StringBuilder sb = new StringBuilder(nu);
            sb.delete(0,12);
            System.out.println(YELLOW  + "Finished! Please look inside the \"Outputs\" folder, and then look inside the " + sb + " folder.");
            String latest = "";
            System.out.println("Please enter whatever student you want to look at.");
            Scanner sin = new Scanner(System.in);
            File di = new File(Main.nu+"/DetailedDocument.txt");
            while (!latest.equalsIgnoreCase("done")) {
                latest=sin.nextLine();
                if (!latest.equalsIgnoreCase("done")) {
                    System.out.println("Looking for data about "+latest+"...");
                    boolean fo = false;
                    Scanner fs = new Scanner(di);
                    while (fs.hasNextLine()) {
                        String name = fs.nextLine();
                        if (name.contains(latest)&&name.contains("Student Name:")) {
                            fo=true;
                            System.out.println("Found student.");
                            System.out.println(name);
                            for (int i = 0; i<17; i++) {
                                System.out.println(fs.nextLine());
                            }
                            break;
                        }
                    }
                    if (!fo) {
                        System.out.println("Couldn't find "+latest+".");
                    }
                    System.out.println("\nPlease enter student, or type 'Done' to exit.");
                }
            }
            System.out.println("Adios!");
        } catch (Exception e) {
            System.out.println("That didn't seem to work. Make sure you spelled the name right, and try again.");
            e.printStackTrace();
            System.exit(0);
        }
    }

    public static void run2023mode() {
        turbo = false;
        try {
            File folda = new File("src/GraduationCSVFiles");
            folda.mkdir();
            File[] matchingFiles = folda.listFiles((dir, name) -> name.endsWith(".csv"));
            new File("src/Outputs").mkdir();
            System.out.println(nu);
            File tem1p = new File(nu);
            System.out.println(tem1p.getAbsolutePath());
            new File(nu).mkdir();
            File curr = new File(nu+"/DetailedDocument.txt");
            curr.createNewFile();
            Scanner in = new Scanner(System.in);
            clear();
            System.out.println(YELLOW + "Hello, and welcome to the Formatting and Outputting program, created by KATZ Studios \nfor Emanon High School/North Cambria District High School. You are currently in "+ YEAR_STYLE+" mode.\nTo input a file, put it into the \"GraduationCSVFiles\"  Folder, and then select it here. Here are your files:\n");
            for (File fop: matchingFiles) {
                System.out.println(GREEN + fop.getName());
            }
            if (matchingFiles.length==0) {
                System.out.println(RED + "It appears you do not have any files ready to use. Please move some .csv files into the \"GraduationCSVFiles\"  Folder, and then try again.");
                System.exit(0);
            }
            System.out.println(YELLOW + "\nPlease enter the file name you wish to use, adding a TUR to the front to use turbo mode." + BLUE);
            String inp;
            File f;
            inp  = in.next();
            if (inp.startsWith("TUR")) {
                turbo = true;
                StringBuilder sb = new StringBuilder(inp);
                sb.delete(0,3);
                inp = sb.toString();
            }
            if (!inp.contains(".csv")) {
                inp+=".csv";
            }
            if (inp.equalsIgnoreCase("s.csv")) {
                inp = "SampleReport.csv";
            }
            f = new File("src/GraduationCSVFiles/" + inp);
            BufferedReader reader = new BufferedReader(new FileReader("src/GraduationCSVFiles/" + inp));
            int lines = -1;
            while (reader.readLine() != null) lines++;
            reader.close();
            int current = 1;
            Scanner s = new Scanner(f);
            String trash = s.nextLine();
            System.out.println(trash);
            ArrayList<Student> honorStud = new ArrayList<>();
            ArrayList<Student> passStud = new ArrayList<>();
            ArrayList<Student> failStud = new ArrayList<>();
            String start = "<html> <head> <title> Emanon High School Graduation Audit </title><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\"> <style> body {background-color:#ffffff;background-image:url(https://lh6.googleusercontent.com/xAd15-3Sp-PXZpxeyUvtYQVgZEZOqZFrTaoLCJYftNc-gbixdwvgt0fmGpcdshwEuQZsiZwxiF82RfD_RbEXblA=w16383);background-repeat:no-repeat;background-position:center left;background-attachment:fixed;} h1{font-family:Arial, sans-serif;letter-spacing:10px;color:#f2c645;background-color:#000000;} p {font-family:Georgia, serif;font-size:14px;font-style:normal;font-weight:normal;color:#ffffff;background-color:#000000;} </style> </head> <body> <h1>EHS GRADUATION PAPER</h1> <p>Kids who graduated with honors: ";
            if (turbo) {
                clear();
                System.out.println(RED + "Turbo mode enabled.");
            }
            while (s.hasNextLine()) {
                if (!turbo) {
                    clear();
                    System.out.println(YELLOW + "Working on student " + current + " of " + lines + "...");
                    current++;
                }
                String line = s.nextLine();
                line = line.replace(" ","");
                String[] data = line.split(",");
                Student javon = new Student(data[1], data[0]);
                DiagnosticFile.writeln("\n\nStudent name: " + javon.getName());
                for (int j = 0; j<data.length; j++) {
                    Grade g = new Grade(data[j]);
                    if (j<48) {
                        int temp = j;
                        while (temp>8) temp-=8;
                        if (temp==2) g.clas=C.MATH;
                        if (temp==3) g.clas=C.ENGLISH;
                        if (temp==4) g.clas=C.SOCIALSTUDIES;
                        if (temp==5) g.clas=C.SCIENCE;
                    } else {
                        if (j==50) g.clas = C.ENGLISH;
                        if (j==51) g.clas = C.SOCIALSTUDIES;
                    }
                    if (g.clas==null) g.clas = C.ELECTIVE;
                    javon.add(g);
                }
                GraduationStatus gr = canGraduate2023(javon);
                if (gr==GraduationStatus.HONORS) {
                    honorStud.add(javon);
                }
                if (gr==GraduationStatus.PASS) {
                    passStud.add(javon);
                }
                if (gr==GraduationStatus.FAIL) {
                    failStud.add(javon);
                }
            }
            Student[] failers = new Student[failStud.size()];
            failers = failStud.toArray(failers);
            clear();
            System.out.println("Sorting failed students...");
            Arrays.sort(failers, Collections.reverseOrder());
            Student[] passers = new Student[passStud.size()];
            passers = passStud.toArray(passers);
            clear();
            System.out.println("Sorting passed students...");
            Arrays.sort(passers, Collections.reverseOrder());
            Student[] honorers = new Student[honorStud.size()];
            honorers = honorStud.toArray(honorers);
            clear();
            System.out.println("Sorting honors students...");
            Arrays.sort(honorers, Collections.reverseOrder());
            StringBuilder allHonorGrad = new StringBuilder();
            clear();
            System.out.println("Creating HTML File...");
            for (int ii = 0; ii<honorers.length; ii++) {
                String en = ", ";
                if (ii==(honorers.length-1)) en = "";
                allHonorGrad.append(honorers[ii].getName()).append(en);
            }
            start+= allHonorGrad + "</p> <p></p> <p>Kids who graduated: ";
            StringBuilder allHonorGradl= new StringBuilder();
            for (int ii = 0; ii<passers.length; ii++) {
                String en = ", ";
                if (ii==(passers.length-1)) en = "";
                allHonorGradl.append(passers[ii].getName()).append(en);
            }
            start+=allHonorGradl+ "</p> <p></p> <p>Kids who did not graduate: ";
            StringBuilder allHonorGradll= new StringBuilder();
            for (int ii = 0; ii<failers.length; ii++) {
                String en = ", ";
                if (ii==(failers.length-1)) en = "";
                allHonorGradll.append(failers[ii].getName()).append(en);
            }
            start+=allHonorGradll+"</p> </body> </html>";
            String fileName = nu+"//Output.html";
            File fi = new File(fileName);
            fi.createNewFile();
            FileWriter fid = new FileWriter(fileName);
            clear();
            System.out.println("Outputting HTML File...");
            fid.write(start);
            fid.close();
            clear();
            StringBuilder sb = new StringBuilder(nu);
            sb.delete(0,12);
            System.out.println(YELLOW  + "Finished! Please look inside the \"Outputs\" folder, and then look inside the " + sb + " folder.");
        } catch (Exception e) {
            System.out.println("That didn't seem to work. Make sure you spelled the name right, and try again.");
            e.printStackTrace();
            System.exit(0);
        }
    }
    public static void clear() {
        System.out.print("\033[H\033[2J");
        System.out.flush();
    }

    public static GraduationStatus canGraduate2024(Student jav) {
        GraduationStatus can = GraduationStatus.PASS;
        if (jav.honorsGrades>=10) {
            can = GraduationStatus.HONORS;
            DiagnosticFile.writeln("Student has enough honors credits to graduate with honors. (Needed: 10, Student has " + jav.honorsGrades + ")");
        }
        if (jav.totalCredits<46) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough credits. (Needed: 46, Student only has " + jav.totalCredits + ")");
        } else DiagnosticFile.writeln("Student has enough credits. (Needed: 46, Student has " + jav.totalCredits + ")");
        if (jav.mathCredits<6) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough math credits. (Needed: 6, Student only has " + jav.mathCredits + ")");
        } else DiagnosticFile.writeln("Student has enough math credits. (Needed: 6, Student has " + jav.mathCredits + ")");
        if (jav.geoCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough geometry credits. (Needed: 2, Student only has " + jav.geoCredits + ")");
        } else DiagnosticFile.writeln("Student has enough geometry credits. (Needed: 2, Student has " + jav.geoCredits + ")");
        if (jav.scienceCredits<6) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough science credits. (Needed: 6, Student only has " + jav.scienceCredits + ")");
        } else DiagnosticFile.writeln("Student has enough science credits. (Needed: 6, Student has " + jav.scienceCredits + ")");
        if (jav.lifeScieCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough biology credits. (Needed: 2, Student only has " + jav.lifeScieCredits + ")");
        } else DiagnosticFile.writeln("Student has enough life biology credits. (Needed: 2, Student has " + jav.lifeScieCredits + ")");
        if (jav.socialStudCredits<7) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough social studies credits. (Needed: 7, Student only has " + jav.socialStudCredits + ")");
        } else DiagnosticFile.writeln("Student has enough social studies credits. (Needed: 7, Student has " + jav.socialStudCredits + ")");
        if (jav.amerGovCredit<1) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have the american government credit. (Needed: 1, Student only has " + jav.amerGovCredit + ")");
        } else DiagnosticFile.writeln("Student has the american government credit. (Needed: 1, Student only has " + jav.amerGovCredit + ")");
        if (jav.amerHistCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough american history credits. (Needed: 2, Student only has " + jav.amerHistCredits + ")");
        } else DiagnosticFile.writeln("Student has enough american history credits. (Needed: 2, Student has " + jav.amerHistCredits + ")");
        if (jav.englishCredits<8) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough english credits. (Needed: 8, Student only has " + jav.englishCredits + ")");
        } else DiagnosticFile.writeln("Student has enough english credits. (Needed: 8, Student has " + jav.englishCredits + ")");
        if (jav.fineArtCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough fine art credits. (Needed: 2, Student only has " + jav.fineArtCredits + ")");
        } else DiagnosticFile.writeln("Student has enough fine art credits. (Needed: 2, Student has " + jav.fineArtCredits + ")");
        if (jav.physEducCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough physical education credits. (Needed: 2, Student only has " + jav.physEducCredits + ")");
        } else DiagnosticFile.writeln("Student has enough physical education credits. (Needed: 2, Student has " + jav.physEducCredits + ")");
        if (jav.speechCredit<1) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have the speech credit. (Needed: 1, Student only has " + jav.speechCredit + ")");
        } else DiagnosticFile.writeln("Student has the speech credit. (Needed: 1, Student has " + jav.speechCredit + ")");
        if (jav.compCredit<1) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have the computers credit. (Needed: 1, Student only has " + jav.speechCredit + ")");
        } else DiagnosticFile.writeln("Student has the computers credit. (Needed: 1, Student has " + jav.speechCredit + ")");
        DiagnosticFile.writeln("Student has an average unweighted GPA of " + (jav.rawGPA/Student.TOTAL_GRADES) + ".");
        DiagnosticFile.writeln("Student has an average weighted GPA of " + (jav.weightGpa/Student.TOTAL_GRADES) + ".");
        DiagnosticFile.writeln("Student has taken " + jav.honorsTaken + " honors classes total.");
        if (jav.honorsTaken==0) jav.honorsTaken=1;
        DiagnosticFile.writeln("Student has an average honors GPA of " + (jav.honorsGPA/jav.honorsTaken) + ".");
        return can;
    }
    public static GraduationStatus canGraduate2023(Student jav) {
        GraduationStatus can = GraduationStatus.PASS;
        if (jav.honorsGrades>=12) {
            can = GraduationStatus.HONORS;
            DiagnosticFile.writeln("Student has enough honors credits to graduate with honors. (Needed: 12, Student has " + jav.honorsGrades + ")");
        }
        if (jav.totalCredits<46) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough credits. (Needed: 46, Student only has " + jav.totalCredits + ")");
        } else DiagnosticFile.writeln("Student has enough credits. (Needed: 46, Student has " + jav.totalCredits + ")");
        if (jav.mathCredits<6) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough math credits. (Needed: 6, Student only has " + jav.mathCredits + ")");
        } else DiagnosticFile.writeln("Student has enough math credits. (Needed: 6, Student has " + jav.mathCredits + ")");
        if (jav.scienceCredits<6) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough science credits. (Needed: 6, Student only has " + jav.scienceCredits + ")");
        } else DiagnosticFile.writeln("Student has enough science credits. (Needed: 6, Student has " + jav.scienceCredits + ")");
        if (jav.lifeScieCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough life science credits. (Needed: 2, Student only has " + jav.lifeScieCredits + ")");
        } else DiagnosticFile.writeln("Student has enough life science credits. (Needed: 2, Student has " + jav.lifeScieCredits + ")");
        if (jav.socialStudCredits<7) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough social studies credits. (Needed: 7, Student only has " + jav.socialStudCredits + ")");
        } else DiagnosticFile.writeln("Student has enough social studies credits. (Needed: 7, Student has " + jav.socialStudCredits + ")");
        if (jav.amerGovCredit<1) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have the american government credit. (Needed: 1, Student only has " + jav.amerGovCredit + ")");
        } else DiagnosticFile.writeln("Student has the american government credit. (Needed: 1, Student only has " + jav.amerGovCredit + ")");
        if (jav.amerHistCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough american history credits. (Needed: 2, Student only has " + jav.amerHistCredits + ")");
        } else DiagnosticFile.writeln("Student has enough american history credits. (Needed: 2, Student has " + jav.amerHistCredits + ")");
        if (jav.englishCredits<7) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough english credits. (Needed: 7, Student only has " + jav.englishCredits + ")");
        } else DiagnosticFile.writeln("Student has enough english credits. (Needed: 2, Student has " + jav.englishCredits + ")");
        if (jav.fineArtCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough fine art credits. (Needed: 2, Student only has " + jav.fineArtCredits + ")");
        } else DiagnosticFile.writeln("Student has enough fine art credits. (Needed: 2, Student has " + jav.fineArtCredits + ")");
        if (jav.physEducCredits<2) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have enough physical education credits. (Needed: 2, Student only has " + jav.physEducCredits + ")");
        } else DiagnosticFile.writeln("Student has enough physical education credits. (Needed: 2, Student has " + jav.physEducCredits + ")");
        if (jav.speechCredit<1) {
            can = GraduationStatus.FAIL;
            DiagnosticFile.writeln("Student does not have the speech credit. (Needed: 1, Student only has " + jav.speechCredit + ")");
        } else DiagnosticFile.writeln("Student has the speech credit. (Needed: 1, Student has " + jav.speechCredit + ")");
        DiagnosticFile.writeln("Student has " + jav.transferCredits + " transfer credit(s).");
        DiagnosticFile.writeln("Student has an average GPA of " + (jav.rawGPA/Student.TOTAL_GRADES) + ".");
        DiagnosticFile.writeln("Student has taken " + jav.honorsTaken + " honors classes total.");
        if (jav.honorsTaken==0) jav.honorsTaken=1;
        DiagnosticFile.writeln("Student has an average honors GPA of " + (jav.honorsGPA/jav.honorsTaken) + ".");
        return can;
    }
}
enum GraduationStatus {
    HONORS,PASS,FAIL
}
class Student implements Comparable<Student> {
    public static final float TOTAL_GRADES = 49; //how many individual grades each person gets
    String firstName = ""; //the student's first name
    String lastName = ""; // the students last name.
    float weightGpa = 0; //this is gpa, but honors classes get +0.5 per grade (exclusive to 2024)
    float rawGPA = 0; // the student's GPA combined. to find real GPA, divide by 49
    float honorsGPA = 0; //the student's honors GPA combined. to find real honors GPA, divide by the total number of honors classes taken
    float honorsTaken = 0; //how many honors classes a student has taken
    int totalCredits = 0; //they need 46 total credits to graduate for both
    int mathCredits; //need 6 for both, but 2024 must include 2 geometry
    int scienceCredits; // 6 semesters of science (must include 2 semesters of life science) for 2023, for 2024: 6 semesters of science (must include 2 semesters of biology)
    int socialStudCredits; //7 semesters of social science (must include 2 semesters of American History and a semester of American Government) for both 2023 and 2024
    int englishCredits; //8 sems for both
    int amerHistCredits; //need 2 for both
    int amerGovCredit; //need 1 for both
    int lifeScieCredits; //need 2 for both, but 2024 calls it Biology
    int physEducCredits; //need 2 for both
    int fineArtCredits; //need 2 for both
    int speechCredit; //need 1 for both, but 2024 calls it public speaking
    int compCredit; //need 1 for 2024
    int geoCredits;//need 2 for 2024
    int honorsGrades; //need 12 to get honors for 2023, need 10 for 2024
    int transferCredits; //only needs these if tied, exclusive to 2023
    public Student(String firsName, String lasName) {
        firstName = firsName;
        lastName = lasName;
    }
    public String getName() {
        return firstName + " " + lastName;
    }
    @Override public int compareTo(Student other) {
        if (Main.YEAR_STYLE==2023) {
            float thGPA = (this.rawGPA/TOTAL_GRADES);
            float othGPA = (other.rawGPA/TOTAL_GRADES);
            if (thGPA>othGPA) return 1;
            if (othGPA>thGPA) return -1;
            if (other.transferCredits<transferCredits) return -1;
            if (other.transferCredits>transferCredits) return 1;
            if (other.honorsGrades>honorsGrades) return -1;
            if (other.honorsGrades<honorsGrades) return 1;
            if (other.totalCredits>totalCredits) return -1;
            if (other.totalCredits<totalCredits) return 1;
            if (other.honorsTaken==0) other.honorsTaken=1;
            if (honorsTaken==0) honorsTaken=1;
            float othgpa = (other.honorsGPA/other.honorsTaken);
            float gpa = (honorsGPA/honorsTaken);
            if (othgpa>gpa) return -1;
            if (gpa>othgpa) return 1;
            String[] arr = new String[]{lastName,other.lastName};
            Arrays.sort(arr);
            if (arr[0].equals(lastName)) return 1; else return -1;
        }
        float thGPA = (this.weightGpa/TOTAL_GRADES);
        float othGPA = (other.weightGpa/TOTAL_GRADES);
        if (thGPA>othGPA) return 1;
        if (othGPA>thGPA) return -1;
        if (other.honorsTaken>honorsTaken) return -1;
        if (other.honorsTaken<honorsTaken) return 1;
        String[] arr = new String[]{lastName,other.lastName};
        Arrays.sort(arr);
        if (arr[0].equals(lastName)) return 1; else return -1;
    }
    public byte getGPA(String let) {
        if (let.equalsIgnoreCase("A")) return 4;
        if (let.equalsIgnoreCase("B")) return 3;
        if (let.equalsIgnoreCase("C")) return 2;
        if (let.equalsIgnoreCase("D")) return 1;
        return 0;
    }
    public float getHonorsGPA(String let) {
        if (let.equalsIgnoreCase("F")) return 0.5f;
        byte gp= getGPA(let);
        if (gp!=0) {
            return ((float)gp)+0.5f;
        }
        return 0;
    }
    public void add(Grade g) {
        if (g.honors) {
            if (Main.YEAR_STYLE==2024) {
                weightGpa+=getHonorsGPA(g.letGrade);
            }
            honorsTaken++;
            byte num = getGPA(g.letGrade);
            honorsGPA+=num;
            if (num>2) honorsGrades++;
        } else {
            if (Main.YEAR_STYLE==2024) {
                weightGpa+=getGPA(g.letGrade);
            }
        }
        rawGPA+=getGPA(g.letGrade);
        String enr = "P";
        if (Main.YEAR_STYLE==2024) enr="enr";
        if (!(g.letGrade.equalsIgnoreCase("F"))) {
            if (!g.encoded.contains(enr)) {
                totalCredits++;
            }
            if (g.transfer) transferCredits++;
            if (g.clas==C.ENGLISH) englishCredits++;
            if (g.clas==C.MATH) mathCredits++;
            if (g.clas==C.SCIENCE) scienceCredits++;
            if (g.clas==C.SOCIALSTUDIES) socialStudCredits++;
            if (g.specClass.equalsIgnoreCase("S")) speechCredit++;
            if (g.specClass.equalsIgnoreCase("AH")) amerHistCredits++;
            if (g.specClass.equalsIgnoreCase("AG")) amerGovCredit++;
            if (g.specClass.equalsIgnoreCase("LS")) lifeScieCredits++;
            if (g.specClass.equalsIgnoreCase("FA")) fineArtCredits++;
            if (g.specClass.equalsIgnoreCase("PE")) physEducCredits++;
            if (g.specClass.equalsIgnoreCase("CO")) compCredit++;
            if (g.specClass.equalsIgnoreCase("GE")) geoCredits++;
        }
    }
}
class Grade {
    C clas; //what class this grade is for
    String encoded; //the encoded grade data
    boolean transfer = false; //is this credit a transfer credit?
    boolean honors = false; //is this credit an honors credit?
    String letGrade; // the letter grade, ex A, B, C, D, F
    String specClass = ""; //if this class is a special class (such as life science) then this holds its special class code
    boolean makeUp = false; //is this a remedial
    public Grade(String g) {
        encoded = g;
        char[] letters = g.toCharArray();
        letGrade = Character.toString(letters[0]);
        if (Main.YEAR_STYLE==2024) {
            if (g.charAt(g.length()-1)=='H') honors=true;
        }
        if (Main.YEAR_STYLE==2023) {
            try {
                int curr = 1;
                if (letters[curr]=='H') {
                    honors = true;
                    curr++;
                } else if (letters[curr]=='T') {
                    transfer = true;
                    curr++;
                }
                if (letters[curr]=='*') {
                    if (letters[curr+1]=='S') {
                        specClass = "S";
                        curr+=2;
                    } else {
                        specClass = Character.toString(letters[curr+1]) + Character.toString(letters[curr+2]);
                        curr+=3;
                    }
                }
                if (letters[curr]=='@') {
                    makeUp = true;
                    if (letters[curr+1]=='M') clas = C.MATH;
                    if (letters[curr+1]=='E') clas = C.ENGLISH;
                    if (letters[curr+1]=='S') {
                        if (letters[curr+2]=='S') clas = C.SOCIALSTUDIES; else clas = C.SCIENCE;
                    }
                }
            } catch (Exception ignored) {}
        }
    }
}
enum C {
    MATH, ENGLISH, SOCIALSTUDIES, SCIENCE, ELECTIVE
}
class DiagnosticFile {
    public static void writeln(String line) {
        try {
            FileWriter kn = new FileWriter(Main.nu+"/DetailedDocument.txt",true);
            kn.write(line+System.getProperty("line.separator"));
            kn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

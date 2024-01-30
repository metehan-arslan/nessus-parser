# nessus-parser
This project is a fork of [Cody Dumont's Nessus Parser](http://www.melcara.com/archives/253). This fork fixes "There is a new plugin family added, it is **_$pluginFamily_**" error by adding the current Plugin Families.  

Feel free to open pull requests/issues!  


## Before Getting Started
- Make sure you have Perl and cpan installed. 
- Get dependencies via cpan:  
>cpan install XML::TreePP Data::Dumper Math::Round Excel::Writer::XLSX Data::Table Excel::Writer::XLSX::Chart Getopt::Std

## Usage

 `perl nessus-parser.pl [-vVhH] [-f file] [-d directory] [-r recast_file (optional) ]`


### Options:
```
    -o      Changes the filename prefix.  The default prefix is "nessus_report".
            A time stamp is appended onto the prefix.  An exmaple of the default
            file name is nessus_report_20130409162908.xlsx.  if the "-o foobar" is
            passed, then the file name will be foobar_20130409162908.xlsx
    
    -d      The target directory where the Nessus V2 XML files are located.
            This option will search the target directory files that end with
            XML, xml, or nessus extentions.  Each file found will be check for
            Nessus V2 XML format.  Each Nessus V2 XML file will be parsed and
            will be stored into an XLSX file.  This option should not be used
            with any other option.

    -f      The target file is a method to call a single file for parsing.
            With this method the XLSX file will be stored in the same folder
            as the XML.  Please note if the path to file has a "SPACE" use
            double quotes around the file path and/or name.

    -r      The Recast option is a feature request from user KurtW.  Kurt wanted
            to be able to change the reported value of Nessus Plugin ID.  While
            this is not recommended in many cases, in some instances the change
            may provide the Nessus user with more accurate report.
            To use this feature create a CSV file with three fields.
            
            Field 1:  Nessus Plugin ID
            Field 2:  Nessus-assigned Severity
            Field 3:  Recasted (User-assigned) Severity
            
            Examples
            
            # Recast vulnerability SSL Certificate Cannot Be Trusted (Plugin ID 51192) from Medium(2) to Critical(4)
            51192,2,4
            
            # Recast vulnerability MySQL 5.1 < 5.1.63 Multiple Vulnerabilities (Plugin ID 59448) from High(3) to Low(1)
            59448,3,1
            
            # Recast vulnerability MS12-067: Vulnerabilities in FAST Search Server 2010 for Sharepoint RCE from High(3) to Critical(4)
            62462,3,4
            
            The file would contain 3 lines.
            51192,2,4
            59448,3,1
            62462,3,4
            
            The command used would be passed the -r recast.txt.  See examples listed below.

    -v      Print this help message.

    -h      Print this help message.
```    


## Examples:

```
        The command:
                perl /path/to/script/nessus-parser.pl -v
            
            This command will print this help message.
-----------------------------------------------------------------------------------------------------------------
        The command:
                perl /path/to/script/nessus-parser.pl -h
            
            This command will print this help message.
-----------------------------------------------------------------------------------------------------------------
        The command:
                perl /path/to/script/nessus-parser.pl -d /foo/bar
            
            This command will seearch the direcoty specified by the "-d" option
            for Nessus XML v2 files and parse the files found.
-----------------------------------------------------------------------------------------------------------------
        The command:
                perl /path/to/script/nessus-parser.pl -f /foo/bar/scan1.nessus
                -----  or -----
                perl /path/to/script/nessus-parser.pl -f /foo/bar/scan1.nessus.xml
            
            This command will seearch the direcoty specified by the "-d" option
            for Nessus XML v2 files and parse the files found.
-----------------------------------------------------------------------------------------------------------------
        The command:
                perl /path/to/script/nessus-parser.pl -f /foo/bar/scan1.nessus -r /path/to/script/recast.txt
```

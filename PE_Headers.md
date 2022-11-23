# PE Header

## What is a PE?
According to Wikipedia:
> The Portable Executable format is a file format for executables, object code, DLLs and others used in 32-bit and 64-bit versions of Windows operating systems. The PE format is a data structure that encapsulates the information necessary for the Windows OS loader to manage the wrapped executable code

So, PE is the Windows executable format.

## What is a PE Header?
A PE Header is essentially a data structure within the PE executable, containing all necessary information for the Windows OS loader to run the executable. It is called the header because it can be found at the beginning (head) of the binary's code.

## What is in a PE Header?
![Credit: InfoSec Institute](https://user-images.githubusercontent.com/44067716/203601055-36a8605a-1261-4254-a2d4-cf20d1b2c9b3.png)

1. **MZ/DOS Header**: Defines the file as an executable
2. **DOS Stub**: Prints "This program cannot be run in DOS mode" if you try to run it in DOS mode, for compatibility purposes.
3. **PE File Header**: Defines the executable type as a PE.
4. **Image_Optional_Header**: It provides essential information to the Windows OS loader, such as the following:
    - SizeOfCode
    - AddressOfEntryPoint (where execution begins, ie start executing from this address in memory)
    - SizeOfHeaders  
5. **Sections Table**: Each section will have a section header containing information such as:
    - Pointer/location of the section
    - Whether or not the section contains data or executable code
    - If the section can be read
    - If the section can be written to. 

As per [Microsoft](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format):
> This table immediately follows the optional header, if any. This positioning is required because the file header does not contain a direct pointer to the section table. Instead, the location of the section table is determined by calculating the location of the first byte after the headers.

Also:
> The number of entries in the section table is given by the NumberOfSections field in the file header. Entries in the section table are numbered starting from one (1). The code and data memory section entries are in the order chosen by the linker.

7. **Sections**: Where the actual code and program data is stored. It is divided up into sections, each with its own set of properties as defined by it's respective Section Header. Below are some example sections, but note that not all sections are always present:
![Image Credit: HackerSploit Malware Analysis Bootcamp](https://user-images.githubusercontent.com/44067716/203605091-b356e711-d370-427a-a03f-16fa824a443d.png)
Note: 
> 1) .idata and .edata may sometimes be within .rdata 
> 2) Common packers like UPX will change the section headers to the name of the packer. so .code or .text becomes .upx , then .upx1, .upx2 and so on.

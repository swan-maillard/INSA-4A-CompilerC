# IFCC - Compiler for a Subset of C

## Description

**IFCC** is a compiler developed to translate source code written in a subset of C into Intel x86 or RISC-V assembly code.

The development of IFCC followed a **Test-Driven Development (TDD)** methodology, ensuring that each component of the compiler is thoroughly tested and validated through a suite of integration tests.

## Usage

### Compiling the IFCC Compiler

To compile IFCC, follow these steps:

1. Ensure you have `make`, as well as `antlr` and its C++ runtime installed on your system. You can install ANTLR using the provided script `install-antlr.sh`.
2. Navigate to the root directory of the IFCC project.
3. Create a `config.mk` file that corresponds to your ANTLR installation, or use one of the provided files: `DI.mk` (installation via the script), `fedora.mk`, `ubuntu.mk`:
   ```bash
   ln -s <file>.mk config.mk
   ```
4. Run the command `make` to build the compiler.

### Compiling a Program

Once IFCC is compiled, you can use it to translate your program written in the supported C subset. Here’s how:

1. Write your program in a file with the `.c` extension.
2. Use the following command to compile your program:

   ```bash
   ./ifcc [-t target] [-o <output_file_name>.s] [-d] [-s] <source_file_name>.c
   ```

   - The `-t target` option allows you to specify the target architecture for assembly generation. You can choose between `x86-64` for Intel x86 and `rv64` for RISC-V. By default, the code is compiled to Intel x86 assembly.
   - The `-o <output_file_name>.s` option specifies the name of the output file for the generated assembly code. By default, the output file name is `./out.s`.
   - The `-s` option displays the generated code in standard output.
   - The `-d` option outputs a representation of the intermediate representation in the error output.

### Assembling and Linking

After generating the assembly code, you need to assemble and link it based on the target architecture. Depending on your machine, you can do the following:

- To assemble and link the assembly code into an executable for Intel x86:

   ```bash
   gcc <source_file_name>.s [-o <executable_name>]
   ```

- To assemble and link the assembly code into an executable for RISC-V:

   ```bash
   riscv64-linux-gnu-gcc <source_file_name>.s [-o <executable_name>]
   ```

   By default, the name of the generated executable is `./a.out`.

### Executing the Program

Once you have the executable, you can run it using the following command:

```bash
./a.out
```

If you compiled for RISC-V and wish to run the program on an emulator, please use the appropriate emulator for the RISC-V architecture.

## Testing

IFCC comes with a suite of integration tests to verify its functionality. The tests are located in the `tests/testfiles/` directory. You can run all tests using the following command:

```bash
make check
```

This will run the tests for both Intel x86 and RISC-V architectures. You can also specify `make check-x86` or `make check-rv64` to run tests for a specific architecture. The TDD approach used during development ensures that all components are thoroughly tested, providing confidence in the compiler's stability and functionality.

## Documentation

The code is documented using Doxygen. To generate the documentation locally, run:

```bash
make doc
```

This will create a comprehensive set of documentation files that you can browse for more detailed information on the compiler's functionality and usage.

## Authors

- BIAUD Alexandre (alexandre.biaud@insa-lyon.fr)
- EL MIR Raoul (raoul.el-mir@insa-lyon.fr)
- HASAN TAWFIQ Amar (amar.hasan-tawfiq@insa-lyon.fr)
- KAROUIA Lilia (lilia.karouia@insa-lyon.fr)
- MAILLARD Swan (maillard.swan@gmail.com)
- PEIGUE Alix (alix.peigue@insa-lyon.fr)

## License

This project is licensed under the MIT License. Please consult the `LICENSE` file for more information.

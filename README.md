# Merge PDFs based on name using Python

## Pasos 🚀

1. Se importan librerias 
2. Define datos directorio de archivos pdf
3. Crear salida
4. Lista
5. Usa las tres llaves
6. Nombre de archivo

## Importar librerías 🔧

  from pathlib import Path
  from PyPDF2 import PdfFileMerger, PdfFileReader  # pip install PyPDF2


## Define input directory for the pdf files 🔩

  pdf_dir = Path(__file__).parent / "pdf_files"

## Define & create output directory 📦

  pdf_output_dir = Path(__file__).parent / "OUPUT"
  pdf_output_dir.mkdir(parents=True, exist_ok=True)

## List all pdf files in the input directory 🔩

  pdf_files = list(pdf_dir.glob("*.pdf"))

## Use the first 3 characters as the 'key' 🔩
## Example of the keys: The 'key' of '902 17.03.2022 2000004496.pdf' is '902'

  keys = set([file.name[:3] for file in pdf_files])

## Determine the file name length of the base file
## Example of the base files: '902 17.03.2022 2000004496.pdf', '904 17.03.2022 2000004497.pdf'

  BASE_FILE_NAME_LENGTH = 20

  for key in keys:
      merger = PdfFileMerger()
      for file in pdf_files:
          if file.name.startswith(key):
              merger.append(PdfFileReader(str(file), "rb"))
              if len(file.name) >= BASE_FILE_NAME_LENGTH:
                  base_file_name = file.name
      merger.write(str(pdf_output_dir / base_file_name))
      merger.close()
      
 ## Autor ✒️
    
⭐️ [fradurgo19](https://github.com/fradurgo19)     

all:
	Rscript -e "knitr::knit('sar.Rmd')"
	pandoc sar.md --reference-docx=template.docx -o sar.docx
	rm sar.md

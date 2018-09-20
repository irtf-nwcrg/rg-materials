BASE=nwcrg_interim_agenda_2018-09-25
MDFILE=${BASE}.md
PDFFILE=${BASE}.pdf
HTMLFILE=${BASE}.html

all:
	# standalone PDF and HTML output
	pandoc -s ${MDFILE} -o ${PDFFILE}
	pandoc -s ${MDFILE} -o ${HTMLFILE}

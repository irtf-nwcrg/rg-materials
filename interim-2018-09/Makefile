BASE=nwcrg_interim_agenda_2018-09-25
BASE2=nwcrg_interim_minutes
MDFILE=${BASE}.md
MDFILE2=${BASE2}.md
PDFFILE=${BASE}.pdf
PDFFILE2=${BASE2}.pdf
HTMLFILE=${BASE}.html

all:
	# standalone PDF and HTML output
	pandoc -s ${MDFILE} -o ${PDFFILE}
	pandoc -s ${MDFILE2} -o ${PDFFILE2}
	#pandoc -s ${MDFILE} -o ${HTMLFILE}
	#pandoc -s ${MDFILE2} -o ${HTMLFILE2}

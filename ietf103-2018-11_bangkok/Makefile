BASE=ietf103_nwcrg_agenda
BASE2=ietf103_nwcrg_minutes
MDFILE=${BASE}.md
MDFILE2=${BASE2}.md
PDFFILE=${BASE}.pdf
PDFFILE2=${BASE2}.pdf
HTMLFILE=${BASE}.html
HTMLFILE2=${BASE2}.html

all:
	# standalone PDF and HTML output
	#pandoc -s ${MDFILE} -o ${PDFFILE}
	pandoc -s ${MDFILE2} -o ${PDFFILE2}
	#pandoc -s ${MDFILE} -o ${HTMLFILE}
	pandoc -s ${MDFILE2} -o ${HTMLFILE2}

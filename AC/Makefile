
# modified  jan 2006 (DC) -Add mini-table of contents to each chapter of html
# modified  01/07/2006 (DC) -Added mini-TOC  to each chapter of html, .latex
# modified  02/01/2006 (DC) -Added new eps: target eps2: is old target.
# modified  02/01/2006 (DC) -Added hi_appendix.latex, supress TOC levels appdix.
# modified  02/01/2006 (DC) - ../bin now included in ACsrc.tar.gz, ACtiny.tar.gz
# modified  02/27/2006 (DC) - Added -z to dvips command in AC.ps target,
# modified  10/01/2006 (DC) - Added Bibliography chapter latex, html; pending: txt,tex groff
# modified  05/28/2007 (DC) - Removed  bibliography to .html, .latex pending for others; .tex, .txt, etc
# modified  10/03/2008 (DC) - Added sml2latx.sed, sml2html.sed to Latex and html sections--
#                           -- to for rebuild for changes to these .sed files.
#                           - see hyperref in hi.latex for pdf hyperlinks.
# modified 08/29/2014 (DC)  - Added ebook support for upub, mobi per Sven Stucki

# 02/10/2006 Failed attempt to set TEXINPUTS path
#Add on to TEX PATH (for tocvsec2.sty) AC.ps:
#Once you get TEXINPUTS set-working you can kill the assigment below
# -It will still work until next boot- clean shell
# If all else fails see hi.latex \usepackage{tocvec2}
# Also try rm -rf AC.* to clear errors
#
# Neither of the following lines works from a clean shell, see hi.latex fix
#TEXINPUTS=$$TEXINPUTS:.:../bin/:
#TEXINPUTS=/home/dennis/lessons/bin/


#This shrinks screen capture height eps:
YRES=108


SRC = basicac.sml \
      complex.sml \
      xzl.sml \
      xzc.sml \
      xzrlc.sml \
      resonant.sml \
      mixed.sml \
      filters.sml \
      trans.sml \
      poly.sml \
      acpower.sml \
      acmeter.sml \
      acmotor.sml \
      lines.sml \
      about.sml \
      contrib.sml \
      dsl.sml \
      hi.tex \
      hi_appendix.latex \
      bye.tex \
      hi.latex \
      bye.latex \
      hi_1.html \
      hi_2.html \
      hi_3.html \
      hi_4.html \
      hi_5.html \
      hi_6.html \
      hi_7.html \
      hi_8.html \
      hi_9.html \
      hi_10.html \
      hi_11.html \
      hi_12.html \
      hi_13.html \
      hi_14.html \
      hi_A1.html \
      hi_A2.html \
      hi_A3.html \
      bye_1.html \
      bye_2.html \
      bye_3.html \
      bye_4.html \
      bye_5.html \
      bye_6.html \
      bye_7.html \
      bye_8.html \
      bye_9.html \
      bye_10.html \
      bye_11.html \
      bye_12.html \
      bye_13.html \
      bye_14.html \
      bye_A1.html \
      bye_A2.html \
      bye_A3.html \
      index.html \
      Makefile

echotex:
	echo "TEXINPUTS= $(TEXINPUTS)"

# Generates HTML output
html : $(SRC) sml2html.sed
	make AC_1.html
	make AC_2.html
	make AC_3.html
	make AC_4.html
	make AC_5.html
	make AC_6.html
	make AC_7.html
	make AC_8.html
	make AC_9.html
	make AC_10.html
	make AC_11.html
	make AC_12.html
	make AC_13.html
	make AC_14.html
	make AC_A1.html
	make AC_A2.html
	make AC_A3.html

#simplify the indexpage for mobi
index_mobi: index.html 
	cat index.html |  sed -e "s+<p></p>++g" \
	-e "s+ - Table of Contents++" \
	-e '/!!!!!!!!!!!!!!!!!/,/<a href="..\/index.htm"/d' \
	-e "s+h3>+p>+g" \
	-e "s+h2>+p>+g" \
	-e "/Master Index/d"  > index_mobi.html


# Converts SubML to html, then into epub and mobi
epub: $(SRC)
	make index_mobi
	#git checkout -- hi_*.html bye_*.html
	if [ !  -d backup ]; then mkdir backup; fi
	# edit header from individual chapters
	cp hi_*.html backup/
	cp bye_*.html backup/
	sed -i '/<a/d' hi_*.html
	sed -i '/<body>/d' hi_*.html
	sed -i '/<hr>/d' hi_*.html
	sed -i '/<h1>Lessons/d' hi_*.html
	# remove footer from chapters
	echo bye_*.html | xargs -n1 cp /dev/null
	# regenerate HTML
	make -B html
	# merge the two consecutive <h1> chapter headers
	# multiline substitution like in http://austinmatzko.com/2008/04/26/sed-multi-line-search-and-replace/
	sed -i -n '1h;1!H;$${;g;s/<h1>\(.*\)<\/h1>.*<h1>\(\&nbsp;\)*\(.*\)<\/h1>/<h1>\1: \U\3\L<\/h1>/g;p;}' AC_*.html
	# generate epub output
	ebook-convert index_mobi.html AC.epub --breadth-first --authors "Tony R. Kuphaldt" --language en --level1-toc //h:h1 --level2-toc //h:h2 --no-default-epub-cover
	ebook-convert index_mobi.html AC.mobi --breadth-first --authors "Tony R. Kuphaldt" --language en --level1-toc //h:h1 --level2-toc //h:h2 --mobi-toc-at-start 
	#restore hi_ bye_ back to original for normal html make
	cp backup/hi_*.html .
	cp backup/bye_*.html .


# Converts SubML source into TeX source
basicac.tex : basicac.sml 
	sed -f sml2tex.sed basicac.sml > basicac.tex

complex.tex : complex.sml
	sed -f sml2tex.sed complex.sml > complex.tex

xzl.tex : xzl.sml
	sed -f sml2tex.sed xzl.sml > xzl.tex

xzc.tex : xzc.sml
	sed -f sml2tex.sed xzc.sml > xzc.tex

xzrlc.tex : xzrlc.sml
	sed -f sml2tex.sed xzrlc.sml > xzrlc.tex

resonant.tex : resonant.sml
	sed -f sml2tex.sed resonant.sml > resonant.tex

mixed.tex : mixed.sml
	sed -f sml2tex.sed mixed.sml > mixed.tex

filters.tex : filters.sml
	sed -f sml2tex.sed filters.sml > filters.tex

trans.tex : trans.sml
	sed -f sml2tex.sed trans.sml > trans.tex

poly.tex : poly.sml
	sed -f sml2tex.sed poly.sml > poly.tex

acpower.tex : acpower.sml
	sed -f sml2tex.sed acpower.sml > acpower.tex

acmeter.tex : acmeter.sml
	sed -f sml2tex.sed acmeter.sml > acmeter.tex

acmotor.tex : acmotor.sml
	sed -f sml2tex.sed acmotor.sml > acmotor.tex

lines.tex : lines.sml
	sed -f sml2tex.sed lines.sml > lines.tex

about.tex : about.sml
	sed -f sml2tex.sed about.sml > about.tex

contrib.tex : contrib.sml
	sed -f sml2tex.sed contrib.sml > contrib.tex

dsl.tex : dsl.sml
	sed -f sml2tex.sed dsl.sml > dsl.tex



# Converts SubML source into LaTeX source
basicac.latex : basicac.sml sml2latx.sed
	sed -f sml2latx.sed basicac.sml > basicac.latex

complex.latex : complex.sml sml2latx.sed
	sed -f sml2latx.sed complex.sml > complex.latex

xzl.latex : xzl.sml sml2latx.sed
	sed -f sml2latx.sed xzl.sml > xzl.latex

xzc.latex : xzc.sml sml2latx.sed
	sed -f sml2latx.sed xzc.sml > xzc.latex

xzrlc.latex : xzrlc.sml sml2latx.sed
	sed -f sml2latx.sed xzrlc.sml > xzrlc.latex

resonant.latex : resonant.sml sml2latx.sed
	sed -f sml2latx.sed resonant.sml > resonant.latex

mixed.latex : mixed.sml sml2latx.sed
	sed -f sml2latx.sed mixed.sml > mixed.latex

filters.latex : filters.sml sml2latx.sed
	sed -f sml2latx.sed filters.sml > filters.latex

trans.latex : trans.sml sml2latx.sed
	sed -f sml2latx.sed trans.sml > trans.latex

poly.latex : poly.sml sml2latx.sed
	sed -f sml2latx.sed poly.sml > poly.latex

acpower.latex : acpower.sml sml2latx.sed
	sed -f sml2latx.sed acpower.sml > acpower.latex

acmeter.latex : acmeter.sml sml2latx.sed
	sed -f sml2latx.sed acmeter.sml > acmeter.latex

acmotor.latex : acmotor.sml sml2latx.sed
	sed -f sml2latx.sed acmotor.sml > acmotor.latex

lines.latex : lines.sml sml2latx.sed
	sed -f sml2latx.sed lines.sml > lines.latex

about.latex : about.sml sml2latx.sed
	sed -f sml2latx.sed about.sml > about.latex
	#no mini-TOC for this chapter-- remove it
	cp about.latex about.latex~
	sed  s/^.minitoc//g about.latex~ >about.latex
	
contrib.latex : contrib.sml sml2latx.sed
	sed -f sml2latx.sed contrib.sml > contrib.latex
	#no mini-TOC for this chapter-- remove it
	cp contrib.latex contrib.latex~
	sed  s/^.minitoc//g contrib.latex~ >contrib.latex
	
dsl.latex : dsl.sml sml2latx.sed
	sed -f sml2latx.sed dsl.sml > dsl.latex
	#no mini-TOC for this chapter-- remove it
	cp dsl.latex dsl.latex~
	sed  s/^.minitoc//g dsl.latex~ >dsl.latex
	


# Converts SubML source into plain ASCII text
basicac.txt : basicac.sml sml2latx.sed
	sed -f sml2txt.sed basicac.sml > basicac.txt

complex.txt : complex.sml
	sed -f sml2txt.sed complex.sml > complex.txt

xzl.txt : xzl.sml
	sed -f sml2txt.sed xzl.sml > xzl.txt

xzc.txt : xzc.sml
	sed -f sml2txt.sed xzc.sml > xzc.txt

xzrlc.txt : xzrlc.sml
	sed -f sml2txt.sed xzrlc.sml > xzrlc.txt

resonant.txt : resonant.sml
	sed -f sml2txt.sed resonant.sml > resonant.txt

mixed.txt : mixed.sml
	sed -f sml2txt.sed mixed.sml > mixed.txt

filters.txt : filters.sml
	sed -f sml2txt.sed filters.sml > filters.txt

trans.txt : trans.sml
	sed -f sml2txt.sed trans.sml > trans.txt

poly.txt : poly.sml
	sed -f sml2txt.sed poly.sml > poly.txt

acpower.txt : acpower.sml
	sed -f sml2txt.sed acpower.sml > acpower.txt

acmeter.txt : acmeter.sml
	sed -f sml2txt.sed acmeter.sml > acmeter.txt

acmotor.txt : acmotor.sml
	sed -f sml2txt.sed acmotor.sml > acmotor.txt

lines.txt : lines.sml
	sed -f sml2txt.sed lines.sml > lines.txt

about.txt : about.sml
	sed -f sml2txt.sed about.sml > about.txt

contrib.txt : contrib.sml
	sed -f sml2txt.sed contrib.sml > contrib.txt

dsl.txt : dsl.sml
	sed -f sml2txt.sed dsl.sml > dsl.txt




# Converts SubML source into HTML source
# toc.map is necessary to htmltoc2 perl script
# added htmltoc2 for mini-table of contnets in chapters
AC_1.html : basicac.sml hi_1.html bye_1.html sml2html.sed
	cat hi_1.html > AC_1.html
	sed -f sml2html.sed basicac.sml >> AC_1.html
	cat bye_1.html >> AC_1.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-\minitoc\-\->" AC_1.html 
AC_2.html : complex.sml hi_2.html bye_2.html sml2html.sed
	cat hi_2.html > AC_2.html
	sed -f sml2html.sed complex.sml >> AC_2.html
	cat bye_2.html >> AC_2.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_2.html

AC_3.html : xzl.sml hi_3.html bye_3.html sml2html.sed
	cat hi_3.html > AC_3.html
	sed -f sml2html.sed xzl.sml >> AC_3.html
	cat bye_3.html >> AC_3.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_3.html

AC_4.html : xzc.sml hi_4.html bye_4.html sml2html.sed
	cat hi_4.html > AC_4.html
	sed -f sml2html.sed xzc.sml >> AC_4.html
	cat bye_4.html >> AC_4.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
       -minitoc "<\!\-\-minitoc\-\->" AC_4.html

AC_5.html : xzrlc.sml hi_5.html bye_5.html sml2html.sed
	cat hi_5.html > AC_5.html
	sed -f sml2html.sed xzrlc.sml >> AC_5.html
	cat bye_5.html >> AC_5.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_5.html

AC_6.html : resonant.sml hi_6.html bye_6.html sml2html.sed
	cat hi_6.html > AC_6.html
	sed -f sml2html.sed resonant.sml >> AC_6.html
	cat bye_6.html >> AC_6.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_6.html

AC_7.html : mixed.sml hi_7.html bye_7.html sml2html.sed
	cat hi_7.html > AC_7.html
	sed -f sml2html.sed mixed.sml >> AC_7.html
	cat bye_7.html >> AC_7.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_7.html

AC_8.html : filters.sml hi_8.html bye_8.html sml2html.sed
	cat hi_8.html > AC_8.html
	sed -f sml2html.sed filters.sml >> AC_8.html
	cat bye_8.html >> AC_8.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
       -minitoc "<\!\-\-minitoc\-\->" AC_8.html

AC_9.html : trans.sml hi_9.html bye_9.html sml2html.sed
	cat hi_9.html > AC_9.html
	sed -f sml2html.sed trans.sml >> AC_9.html
	cat bye_9.html >> AC_9.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_9.html

AC_10.html : poly.sml hi_10.html bye_10.html sml2html.sed
	cat hi_10.html > AC_10.html
	sed -f sml2html.sed poly.sml >> AC_10.html
	cat bye_10.html >> AC_10.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_10.html

AC_11.html : acpower.sml hi_11.html bye_11.html sml2html.sed
	cat hi_11.html > AC_11.html
	sed -f sml2html.sed acpower.sml >> AC_11.html
	cat bye_11.html >> AC_11.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_11.html

AC_12.html : acmeter.sml hi_12.html bye_12.html sml2html.sed
	cat hi_12.html > AC_12.html
	sed -f sml2html.sed acmeter.sml >> AC_12.html
	cat bye_12.html >> AC_12.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_12.html

AC_13.html : acmotor.sml hi_13.html bye_13.html sml2html.sed
	cat hi_13.html > AC_13.html
	sed -f sml2html.sed acmotor.sml >> AC_13.html
	cat bye_13.html >> AC_13.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_13.html

AC_14.html : lines.sml hi_14.html bye_14.html sml2html.sed
	cat hi_14.html > AC_14.html
	sed -f sml2html.sed lines.sml >> AC_14.html
	cat bye_14.html >> AC_14.html
	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map \
        -minitoc "<\!\-\-minitoc\-\->" AC_14.html

AC_A1.html : about.sml hi_A1.html bye_A1.html sml2html.sed
	cat hi_A1.html > AC_A1.html
	sed -f sml2html.sed about.sml >> AC_A1.html
	cat bye_A1.html >> AC_A1.html
#	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map AC_A1.html


AC_A2.html : contrib.sml hi_A2.html bye_A2.html sml2html.sed
	cat hi_A2.html > AC_A2.html
	sed -f sml2html.sed contrib.sml >> AC_A2.html
	cat bye_A2.html >> AC_A2.html
#	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map AC_A2.html

AC_A3.html : dsl.sml hi_A3.html bye_A3.html sml2html.sed
	cat hi_A3.html > AC_A3.html
	sed -f sml2html.sed dsl.sml >> AC_A3.html
	cat bye_A3.html >> AC_A3.html
#	./htmltoc2 -inline -noorg  -toclabel " " -tocmap toc.map AC_A3.html



# Generates DVI output using TeX
tex : $(SRC)
	make basicac.tex
	make complex.tex
	make xzl.tex
	make xzc.tex
	make xzrlc.tex
	make resonant.tex
	make mixed.tex
	make filters.tex
	make trans.tex
	make poly.tex
	make acpower.tex
	make acmeter.tex
	make acmotor.tex
	make lines.tex
	make about.tex
	make contrib.tex
	make dsl.tex
	cat hi.tex \
           basicac.tex \
           complex.tex \
           xzl.tex \
           xzc.tex \
           xzrlc.tex \
           resonant.tex \
           mixed.tex \
           filters.tex \
           trans.tex \
           poly.tex \
           acpower.tex \
           acmeter.tex \
           make acmotor.tex \
           make lines.tex \
           about.tex \
           contrib.tex \
           dsl.tex \
           bye.tex > AC.tex
	tex AC.tex
	touch tex



# Generates DVI output using LaTeX
latex : $(SRC) sml2latx.sed
	make basicac.latex
	make complex.latex
	make xzl.latex
	make xzc.latex
	make xzrlc.latex
	make resonant.latex
	make mixed.latex
	make filters.latex
	make trans.latex
	make poly.latex
	make acpower.latex
	make acmeter.latex
	make acmotor.latex
	make lines.latex
	make about.latex
	make contrib.latex
	make dsl.latex
	cat hi.latex \
           basicac.latex \
           complex.latex \
           xzl.latex \
           xzc.latex \
           xzrlc.latex \
           resonant.latex \
           mixed.latex \
           filters.latex \
           trans.latex \
           poly.latex \
           acpower.latex \
           acmeter.latex \
           acmotor.latex \
           lines.latex \
           hi_appendix.latex \
           about.latex \
           contrib.latex \
           dsl.latex \
           bye.latex > AC.latex

	latex AC.latex
	makeindex AC.idx
	latex AC.latex
	latex AC.latex
	touch latex


# Generates plain ASCII output
txt : $(SRC)
	make basicac.txt
	make complex.txt
	make xzl.txt
	make xzc.txt
	make xzrlc.txt
	make resonant.txt
	make mixed.txt
	make filters.txt
	make trans.txt
	make poly.txt
	make acpower.txt
	make acmeter.txt
	make acmotor.txt
	make lines.txt
	make about.txt
	make contrib.txt
	make dsl.txt
	cat basicac.txt \
           complex.txt \
           xzl.txt \
           xzc.txt \
           xzrlc.txt \
           resonant.txt \
           mixed.txt \
           filters.txt \
           trans.txt \
           poly.txt \
           acpower.txt \
           acmeter.txt \
           about.txt \
           contrib.txt \
           dsl.txt > AC.txt
	touch txt




# Generates compressed PostScript and PDF output
AC.ps : $(SRC)
	make latex
	dvips -z -Ppdf -o AC.ps AC.dvi
	ps2pdf AC.ps AC.pdf
	gzip -f AC.ps




# Converts schematic and equation .eps graphics into .png format
png: $(SRC)
	mogrify -density 120 -format png 0*.eps
	mogrify -density 120 -format png 1*.eps
	touch png




# Converts photograph .jpg graphics into .eps format
# Don't have png2eps? Then use eps2: target instead of eps: target It
# only needs mogrify. But images files are larger, Images not as nice.
# This (eps2: or eps:) is only required for TeX/LaTeX.

eps2: $(SRC)
#	mogrify -density 175 -format eps 2*.png # poor spice eps 10/31/1005 (DC)
	mogrify -density 20 -format eps 2*.png  # make a clean image (DC)
	mogrify -resize 24% -format eps 2*.eps  # make it smaller (DC)

	mogrify -density 175 -format eps 4*.jpg
	mogrify -density 175 -format eps 5*.jpg
	touch eps

# Convert *.jpg to .eps -smaller .eps files than above, alternative to above


eps: $(SRC)
	YRES=108  #Y resolution to shrink height, 72 normal
	for file in 2*.png; do \
	../bin/png2eps $$file $(YRES) >`echo $$file | sed -ne 's/png/eps/p;'`; \
	done

	for file in 5*.jpg; do \
	cp $$file $$file'~' ; \
	done

	for file in 4*.jpg; do \
	cp $$file $$file'~' ; \
	done

#       jpeg2eps makes bigger eps's from jpg, so shrink them       
####	mogrify -scale 42% -format jpeg 4*.jpg~
####	mogrify -scale 42% -format jpeg 5*.jpg~

	../bin/jpeg2eps 4*.jpg
	../bin/jpeg2eps 5*.jpg


#	for file in 5*.eps; do \
#	cp $$file $$file'~' ; \
#	done

	for file in 4*.eps; do \
	cp $$file $$file'~' ; \
	done

	for file in 5*.eps; do \
	cp $$file $$file'~' ; \
	done

	for file in 4*.eps; do \
	../bin/./scale.sh 50% $$file'~' $$file ; \
	done

	for file in 5*.eps; do \
	../bin/./scale.sh 50% $$file'~' $$file ; \
	done


#	rm [45]2*.jpeg
	rm 42*.jpg~
	rm 52*.jpg~
	rm 42*.eps~
	rm 52*.eps~
	touch eps



# Generates a .tar.gz archive containing source files
ACsrc.tar.gz: $(SRC)
	tar cvf ACsrc.tar \
            $(SRC) \
            *.eps \
            *.jpg \
            *.png \
            *.lps \
            *.sed \
            toc.map \
            htmltoc2 \
            Makefile
	gzip -f ACsrc.tar




# Generates a .tar.gz archive containing only ESSENTIAL source files
ACtiny.tar.gz: $(SRC)
	tar cvf ACtiny.tar \
            $(SRC) \
            0*.eps \
            1*.eps \
            2*.png \
            4*.jpg \
            5*.jpg \
            previous.jpg \
            contents.jpg \
            next.jpg \
            ps.* \
            pdf.* \
            book-02.png \
            src1.* \
            src2.* \
            *.lps \
            *.sed \
            toc.map \
            htmltoc2 \
            Makefile
	gzip -f ACtiny.tar


# Cleans out old, unwanted files
clean:
	-rm *.bak
	-rm *.spn
	-rm junk*
	-rm core


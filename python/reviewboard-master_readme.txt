bzr; python_version == '2.7'
kgb>=4.0
mercurial>=4.4.2; python_version == '2.7'
mock
nose
p4python
setuptools>=18.2
subvertpy
wheel
beanbag-docutils>=1.4
Sphinx>=1.7,<=1.999
Review Board
============

`Review Board`_ is an open source, web-based code and document review tool
built to help companies, open source projects, and other organizations keep
their quality high and their bug count low.

We began writing Review Board in 2006 to fill a hole in the code review market.
We wanted something open source that could be flexible enough to work with a
variety of workflows, and could take the pain out of the code review process.

Today, it's a vital part of the development process at thousands of projects
and companies, ranging from small startups of two people to enterprises of
thousands.

.. _`Review Board`: https://www.reviewboard.org/


What does Review Board do?
--------------------------

Review Board tracks changes to your pending code, graphics, documents, and all
discussions around all the decisions made about your product. Our diff viewer
does more than just display diffs: It shows you exactly how your code was
changed, with syntax highlighting, interdiffs, moved line detection,
indentation change indicators, and more.

You can integrate with Review Board using its rich API and extension
frameworks, allowing custom features, review UIs, data analysis, and more to be
built without ever having to fork Review Board.

There's support for Bazaar, ClearCase, CVS, Git, Mercurial, Perforce, Plastic,
and Team Foundation Server, hosted on your own server or on Assembla,
Beanstalk, Bitbucket, Codebase, GitHub, GitLab, Gitorious, Kiln, or Unfuddle.

To learn more, visit the `Review Board website`_.

.. _`Review Board website`: https://www.reviewboard.org/


Setting up Review Board
-----------------------

First, `get Review Board <https://www.reviewboard.org/get/>`_. Our helpful
interactive guide will walk you through what you need to download and install
Review Board.

We can also host Review Board for you at RBCommons_. Management is simple,
and we'll take care of all the administrative work.

If you want to get a feel for Review Board, check out the demo_.

For additional information, see our documentation:

* `Review Board User Manual`_
* `Review Board Administration Manual`_
* FAQ_

.. _RBCommons: https://rbcommons.com/
.. _demo: http://demo.reviewboard.org/
.. _`Review Board User Manual`:
   https://www.reviewboard.org/docs/manual/latest/users/
.. _`Review Board Administration Manual`:
   https://www.reviewboard.org/docs/manual/latest/admin/
.. _FAQ: https://www.reviewboard.org/docs/manual/latest/faq/


Installing Power Pack
---------------------

`Power Pack`_ extends Review Board, adding such helpful features as:

* `Report generation`_
* `PDF document review`_
* Better multi-server scalability
* Integration with `Microsoft Team Foundation Server`_
* Integration with `GitHub Enterprise`_
* LDAP/Active Directory user sync (coming soon)

To get started, `download a trial license`_, or read the
`Power Pack documentation`_ for more information.

.. _`Power Pack`: https://www.reviewboard.org/powerpack/
.. _`Report generation`:
   https://www.reviewboard.org/docs/powerpack/latest/powerpack/manual/reports/
.. _`PDF document review`:
   https://www.reviewboard.org/docs/powerpack/latest/powerpack/manual/pdf/
.. _`Microsoft Team Foundation Server`:
   https://www.visualstudio.com/en-us/products/tfs-overview-vs.aspx
.. _`GitHub Enterprise`: https://enterprise.github.com/
.. _`download a trial license`: https://www.reviewboard.org/powerpack/trial/
.. _`Power Pack documentation`:
   https://www.reviewboard.org/docs/powerpack/latest/


Installing RBTools
------------------

If you're an end-user already using Review Board, you'll want to install
RBTools, our command line suite for working with Review Board.

RBTools makes it easy to post changes for review, land reviewed changes,
patch your local tree with someone else's changes, check your workload, and
much more.

RBTools can be `installed <https://www.reviewboard.org/downloads/rbtools/>`_
on Windows, Linux, Mac, and other platforms. See the `RBTools documentation`_
for everything it can do.

.. _`RBTools documentation`: https://www.reviewboard.org/docs/rbtools/latest/


Getting Support
---------------

We can help you get going with Review Board, and diagnose any issues that may
come up. There are two levels of support: Public community support, and private
premium support.

The public community support is available on our main `discussion list`_. We
generally respond to requests within a couple of days. This support works well
for general, non-urgent questions that don't need to expose confidential
information.

We can also provide more
`dedicated, private support <https://www.beanbaginc.com/support/contracts/>`_
for your organization through a support contract. We offer same-day responses
(generally within a few hours, if not sooner), confidential communications,
installation/upgrade assistance, emergency database repair, phone/chat (by
appointment), priority fixes for urgent bugs, and backports of urgent fixes to
older releases (when possible).

.. _`discussion list`: https://groups.google.com/group/reviewboard/


Our Happy Users
---------------

There are thousands of companies and organizations using Review Board today.
We respect the privacy of our users, but some of them have asked to feature them
on the `Happy Users page`_.

If you're using Review Board, and you're a happy user,
`let us know! <https://groups.google.com/group/reviewboard/>`_.


.. _`Happy Users page`: https://www.reviewboard.org/users/


Reporting Bugs
--------------

Hit a bug? Let us know by
`filing a bug report <https://www.reviewboard.org/bugs/new/>`_.

You can also look through the
`existing bug reports <https://www.reviewboard.org/bugs/>`_ to see if anyone
else has already filed the bug.


Contributing
------------

Are you a developer? Do you want to integrate with Review Board, or work on
Review Board itself? Great! Let's help you get started.

First off, we have a few handy guides:

* `Web API Guide`_
* `Extending Review Board`_
* `Contributor Guide`_

We accept patches to Review Board, RBTools, and other related projects on
`reviews.reviewboard.org <https://reviews.reviewboard.org/>`_. (Please note
that we do not accept pull requests.)

Got any questions about anything related to Review Board and development? Head
on over to our `development discussion list`_.

.. _`Web API Guide`: https://www.reviewboard.org/docs/manual/latest/webapi/
.. _`Extending Review Board`:
   https://www.reviewboard.org/docs/manual/latest/webapi
.. _`Contributor Guide`: https://www.reviewboard.org/docs/codebase/dev/
.. _`development discussion list`:
   https://groups.google.com/group/reviewboard-dev/


Related Projects
----------------

* Djblets_ -
  Our pack of Django utilities for datagrids, API, extensions, and more. Used
  by Review Board.
* RBTools_ -
  The RBTools command line suite.
* ReviewBot_ -
  Pluggable, automated code review for Review Board.
* rb-gateway_ -
  Manages Git repositories, providing a full API enabling all of Review Board's
  feaures.

.. _Djblets: https://github.com/djblets/djblets/
.. _RBTools: https://github.com/reviewboard/rbtools/
.. _ReviewBot: https://github.com/reviewboard/ReviewBot/
.. _rb-gateway: https://github.com/reviewboard/rb-gateway/

 U T F - 1 6 l e   e n c o d e d   s a m p l e   p l a i n - t e x t   f i l e 
 > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > > 
 
 M a r k u s   K u h n   [ m a k s   k u n ]   < h t t p : / / w w w . c l . c a m . a c . u k / ~ m g k 2 5 / >      2 0 0 2 - 0 7 - 2 5 
 
 
 T h e   A S C I I   c o m p a t i b l e   U T F - 8   e n c o d i n g   u s e d   i n   t h i s   p l a i n - t e x t   f i l e 
 i s   d e f i n e d   i n   U n i c o d e ,   I S O   1 0 6 4 6 - 1 ,   a n d   R F C   2 2 7 9 . 
 
 
 U s i n g   U n i c o d e / U T F - 8 ,   y o u   c a n   w r i t e   i n   e m a i l s   a n d   s o u r c e   c o d e   t h i n g s   s u c h   a s 
 
 M a t h e m a t i c s   a n d   s c i e n c e s : 
 
     ."  E "d a   =   Q ,     n   !  ",   "  f ( i )   =   "  g ( i ) ,             ###% % % % % %%###
                                                                                         ###%a  + b    ###
      "x "!:   #x 	#  =   "
#"x #,     '"     =    (    ("  ) ,         ###% % % % % %  ###
                                                                                         ####  c        ###
     !  "  !   "  $!  "  !  "  !  "  !,                                       ###              ###
                                                                                         ###  "          ###
     "  <   a   `"  b   a"  c   d"  d   j"  "  !  ( 'A '  !  'B ') ,             ###  #          ###
                                                                                         ###  #a q - b q ###
     2 H    +   O    !  2 H  O ,   R   =   4 . 7   k ,    #  2 0 0   m m           ###i = 1         ###
 
 L i n g u i s t i c s   a n d   d i c t i o n a r i e s : 
 
      i   1n t Yn  Yn Yl   f Yn [t 1k   Ys o s i e 1n 
     Y   [ p s i l Tn ] ,   Y e n   [ j [n ] ,   Y o g a   [ j o g Q] 
 
 A P L : 
 
     ( ( V s#V ) = s#t#V ) / V !, V         7#!s#!t#"""> N#U##
 
 N i c e r   t y p o g r a p h y   i n   p l a i n   t e x t   f i l e s : 
 
     T%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%W%
     Q%                                                                                    Q%
     Q%      "    s i n g l e    a n d    d o u b l e    q u o t e s                   Q%
     Q%                                                                                    Q%
     Q%      "   C u r l y   a p o s t r o p h e s :    W e  v e   b e e n   h e r e    Q%
     Q%                                                                                    Q%
     Q%      "   L a t i n - 1   a p o s t r o p h e   a n d   a c c e n t s :   '  `     Q%
     Q%                                                                                    Q%
     Q%      "    d e u t s c h e     A n f  h r u n g s z e i c h e n                Q%
     Q%                                                                                    Q%
     Q%      "     ,   ! ,   0 ,   " ,   3  4 ,    ,   "5 / + 5 ,   "!,   &             Q%
     Q%                                                                                    Q%
     Q%      "   A S C I I   s a f e t y   t e s t :   1 l I | ,   0 O D ,   8 B           Q%
     Q%                                            m% % % % % % % % % %n%                  Q%
     Q%      "   t h e   e u r o   s y m b o l :   %  1 4 . 9 5      %                  Q%
     Q%                                            p% % % % % % % % % %o%                  Q%
     Z%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%P%]%
 
 C o m b i n i n g   c h a r a c t e r s : 
 
     S T A R G 
T E   S G - 1 ,   a   =   v   =   r ,   a    "  b  
 
 G r e e k   ( i n   P o l y t o n i c ) : 
 
     T h e   G r e e k   a n t h e m : 
 
     r  w   x  t  y
         t  u, 
     r  w   x  t  D
     z  r  w  q  t  . 
 
       p  y  s
       u  p  1q
     v  p     s
     ,   f  ,   q! 
 
     F r o m   a   s p e e c h   o f   D e m o s t h e n e s   i n   t h e   4 t h   c e n t u r y   B C : 
 
     Pv  Pp  ww    },   f    , 
     E    0  p  q   s  v  E  x  z
     y  S   {  z  r  p  y  v  
     u  w  A  s,   p  r  q
     0    u,     e  E  t  y  Pv
     y    s  s.   Ps  V      
     1  p    s  "  t  Qy,   v  '  {, 
     Pv  t  V  q  Q  q.   |  s,   E  s
           y  v  p  Q       v  w
     u,   v  q     6      q,   P  q
     s     y    s  s    1x
       !  6  t  },   E  z  q
     }.   p  p    w  Qq,   y  v  v  
     w  uw    v  C  y  s    v  r
     t   t  @  Qs,   q  !  v  
       A    y. 
 
     s,     x
 
 G e o r g i a n : 
 
     F r o m   a   U n i c o d e   c o n f e r e n c e   i n v i t a t i o n : 
 
             U n i c o d e -     
       ,       1 0 - 1 2   , 
     .   ,   .         
                 U n i c o d e - , 
         ,   U n i c o d e -   
       ,       ,   , 
               . 
 
 R u s s i a n : 
 
     F r o m   a   U n i c o d e   c o n f e r e n c e   i n v i t a t i o n : 
 
     0@538AB@8@C9B5AL  A59G0A  =0  5AOBCN  564C=0@>4=CN  >=D5@5=F8N  ?>
     U n i c o d e ,   :>B>@0O  A>AB>8BAO  1 0 - 1 2   <0@B0  1 9 9 7   3>40  2  09=F5  2  5@<0=88. 
     >=D5@5=F8O  A>15@5B  H8@>:89  :@C3  M:A?5@B>2  ?>    2>?@>A0<  3;>10;L=>3>
     =B5@=5B0  8  U n i c o d e ,   ;>:0;870F88  8  8=B5@=0F8>=0;870F88,   2>?;>I5=8N  8
     ?@8<5=5=8N  U n i c o d e   2  @07;8G=KE  >?5@0F8>==KE  A8AB5<0E  8  ?@>3@0<<=KE
     ?@8;>65=8OE,   H@8DB0E,   25@AB:5  8  <=>3>O7KG=KE  :><?LNB5@=KE  A8AB5<0E. 
 
 T h a i   ( U C S   L e v e l   2 ) : 
 
     E x c e r p t   f r o m   a   p o e t r y   o n   T h e   R o m a n c e   o f   T h e   T h r e e   K i n g d o m s   ( a   C h i n e s e 
     c l a s s i c   ' S a n   G u a ' ) : 
 
     [ - - - - - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - - - - - - - - - - - ] 
         O  AH4.1H@*7H-!B#!A**1@'
    #0@(-9J9I6IC+!H
     *4*-)1#4"LH-+I2A%1D              *--LD#IBH@%2@21

2
         #17-15@G5H6H                      I2@!7-6'4#4@G1+2
     B.4K@#5"11H'+1'@!7-!2                  +!2"0H2!
1H'1'*31

         @+!7-1D*D%H@*7-2@+2            #1+!2H2@I2!2@%"-2*1

     H2"-I--8I"8A"C+IA1                    C
I*2'1I@G
'
7H
'C
         %1%4	8"8"5%1H-@+8                    
H2-2@(#4+2I2#I-D+I
     I-##2H21##%1"                      $E+2C#I3
99I##%1L  /
 
     ( T h e   a b o v e   i s   a   t w o - c o l u m n   t e x t .   I f   c o m b i n i n g   c h a r a c t e r s   a r e   h a n d l e d 
     c o r r e c t l y ,   t h e   l i n e s   o f   t h e   s e c o n d   c o l u m n   s h o u l d   b e   a l i g n e d   w i t h   t h e 
     |   c h a r a c t e r   a b o v e . ) 
 
 E t h i o p i a n : 
 
     P r o v e r b s   i n   t h e   A m h a r i c   l a n g u a g e : 
 
     0  s(5  	%  05b
     e    ct  `F b
     %  dq  A%  b
        `
  Ed  c #  #u  `b
     M  s  `Ed  s=b
     %  ``    psb
     2p(	  (
b
     @5  `@5e  A
  `
)  
b
     -  be-  `3  5-b
     0  dq      	(dq  p-b
     
-  Hp  	..  3  -b
     (du  ce  bu  5E  cu   
Eb
     %+  Msu  
  Ksub
     c  *  e  
    +
b
     5  )    +  )  -b
     p  bpI  p
6  cIb
       -  b  (-5  u0b
     
-  `M+=  
  -b
 
 R u n e s : 
 
                           
 
     ( O l d   E n g l i s h ,   w h i c h   t r a n s c r i b e d   i n t o   L a t i n   r e a d s   ' H e   c w a e t h   t h a t   h e 
     b u d e   t h a e m   l a n d e   n o r t h w e a r d u m   w i t h   t h a   W e s t s a e . '   a n d   m e a n s   ' H e   s a i d 
     t h a t   h e   l i v e d   i n   t h e   n o r t h e r n   l a n d   n e a r   t h e   W e s t e r n   S e a . ' ) 
 
 B r a i l l e : 
 
     L(('((  <(((    M((((9(0((  c(((
 
     M((((9(  :(((  (((((  ((  ((((  :(
(9(2(  y(;((  
((  ((  (3(((
     1(((('(;(  ((3((  9(((2(  y((  (((
((;(  ((  (
((  (%((
(((  :(((
     (
(((+(  (9(  9((  
((;((9(
((((  9((  
((;(((  9((  %(((;((((;((
     (((  9((  !(
(((  
(3(((;(2(  N(
((((((  (
(((+(  
((2(  A(((
     N(
((((((0((  ((
((  :(((  ((((  %((((  0(a((((((  (((  ((9(9(((  ((
     !((((  ((  (%((  (
((  ((((  ((2(
 
     U(((  M((((9(  :(((  ((  ((((  ((  (  (((($(((
((2(
 
     M((((  J(  (((0((  
((((  ((  ((9(  9(((  J(  ((*((  ((  
(9(
     *((  ((*((+((((  1(((  9(;((  
((  (((
(
(%((((9(  ((((  ((3((
     (  (((($(((
((2(  J(  
(
(#((  (('((  ((2(  (
(((+((  
(9((((((  ((
     (((((  (  
((((($(((
((  ((  9((  ((((((  (
((
((  ((  
((((
((((;(9(
     (  9((  (((((2(  C(%((  9((  :(
((((
(  ((  3((  ((
((((((
     
((  (  9((  (
(
(
((((  (((  
(9(  %((((((*(+(  (((((
     )((((  (((  (
((%(((  
(((  ((  9((  J(3((((9(0((  ((((  (((2(  y(3(
     :(
(((  9(;((((((  (;(
(
((  
((  ((  (((((((  (
(((((
(
((((9((  9(((
     M((((9(  :(((  ((  ((((  ((  (  (((($(((
((2(
 
     ( T h e   f i r s t   c o u p l e   o f   p a r a g r a p h s   o f   " A   C h r i s t m a s   C a r o l "   b y   D i c k e n s ) 
 
 C o m p a c t   f o n t   s e l e c t i o n   e x a m p l e   t e x t : 
 
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z   / 0 1 2 3 4 5 6 7 8 9 
     a b c d e f g h i j k l m n o p q r s t u v w x y z              
             " & 0 "!S`x~     01234
      """!'"*"a""  !!!!!  %<%T%X%%%:&@&  @$  PN#1
 
 G r e e t i n g s   i n   v a r i o u s   l a n g u a g e s : 
 
     H e l l o   w o r l d ,   s  y,   00000
 
 B o x   d r a w i n g   a l i g n m e n t   t e s t s :                                                                                     %
                                                                                                                                             %
     T%P%P%f%P%P%W%    % % %,% % %%    m% % %,% % %n%    m% % %,% % %n%    %%%3%%%%    %%%%      w%    {%  %/%%  %0%%        %  q%r%q%r%s%s%s%
     Q%% %h% %%Q%    %T%P%g%P%W%%    %R%P%j%P%U%%    %S% %A% %V%%    %% %B% %%%    %C%D%%    v%<%t%z%K%x% %<%(%  %K%%%        %  r%q%r%q%s%s%s%
     Q%%r%  q%%Q%    %Q%      Q%%    %%  %  %%    %Q%  %  Q%%    %%  %  %%    
%E%F%%      u%    y%  %7%%  %8%%        %  q%r%q%r%s%s%s%
     `%a%  s%  ^%c%    %b%      _%$%    %<% %<% %<%$%    %k% %B% %k%$%    #%?%~%<%|%?%+%    %%%%          %%%%  N%  %%%%  %  %  r%q%r%q%s%s%s%
     Q%%q%  r%%Q%    %Q%      Q%%    %%  %  %%    %Q%  %  Q%%    %%  }%  %%    %%%%%%%%  
%    %  N%  O%    %  %  %
     Q%% %e% %%Q%    %Z%P%d%P%]%%    %X%P%j%P%[%%    %Y% %@% %\%%    %% %B% %%%    %%%%%%%%  
%    %  N%  O%    %  %  %
     Z%P%P%i%P%P%]%    % % %4% % %%    p% % %4% % %o%    p% % %4% % %o%    %%%;%%%%    %%%%%%      %L%L%%  N%  %M%M%%  %    %%%%%%%%
                                                                                               %%%%%%
                     GNU GENERAL PUBLIC LICENSE
                       Version 2, June 1991

 Copyright (C) 1989, 1991 Free Software Foundation, Inc.,
 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.

                            Preamble

  The licenses for most software are designed to take away your
freedom to share and change it.  By contrast, the GNU General Public
License is intended to guarantee your freedom to share and change free
software--to make sure the software is free for all its users.  This
General Public License applies to most of the Free Software
Foundation's software and to any other program whose authors commit to
using it.  (Some other Free Software Foundation software is covered by
the GNU Lesser General Public License instead.)  You can apply it to
your programs, too.

  When we speak of free software, we are referring to freedom, not
price.  Our General Public Licenses are designed to make sure that you
have the freedom to distribute copies of free software (and charge for
this service if you wish), that you receive source code or can get it
if you want it, that you can change the software or use pieces of it
in new free programs; and that you know you can do these things.

  To protect your rights, we need to make restrictions that forbid
anyone to deny you these rights or to ask you to surrender the rights.
These restrictions translate to certain responsibilities for you if you
distribute copies of the software, or if you modify it.

  For example, if you distribute copies of such a program, whether
gratis or for a fee, you must give the recipients all the rights that
you have.  You must make sure that they, too, receive or can get the
source code.  And you must show them these terms so they know their
rights.

  We protect your rights with two steps: (1) copyright the software, and
(2) offer you this license which gives you legal permission to copy,
distribute and/or modify the software.

  Also, for each author's protection and ours, we want to make certain
that everyone understands that there is no warranty for this free
software.  If the software is modified by someone else and passed on, we
want its recipients to know that what they have is not the original, so
that any problems introduced by others will not reflect on the original
authors' reputations.

  Finally, any free program is threatened constantly by software
patents.  We wish to avoid the danger that redistributors of a free
program will individually obtain patent licenses, in effect making the
program proprietary.  To prevent this, we have made it clear that any
patent must be licensed for everyone's free use or not licensed at all.

  The precise terms and conditions for copying, distribution and
modification follow.

                    GNU GENERAL PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. This License applies to any program or other work which contains
a notice placed by the copyright holder saying it may be distributed
under the terms of this General Public License.  The "Program", below,
refers to any such program or work, and a "work based on the Program"
means either the Program or any derivative work under copyright law:
that is to say, a work containing the Program or a portion of it,
either verbatim or with modifications and/or translated into another
language.  (Hereinafter, translation is included without limitation in
the term "modification".)  Each licensee is addressed as "you".

Activities other than copying, distribution and modification are not
covered by this License; they are outside its scope.  The act of
running the Program is not restricted, and the output from the Program
is covered only if its contents constitute a work based on the
Program (independent of having been made by running the Program).
Whether that is true depends on what the Program does.

  1. You may copy and distribute verbatim copies of the Program's
source code as you receive it, in any medium, provided that you
conspicuously and appropriately publish on each copy an appropriate
copyright notice and disclaimer of warranty; keep intact all the
notices that refer to this License and to the absence of any warranty;
and give any other recipients of the Program a copy of this License
along with the Program.

You may charge a fee for the physical act of transferring a copy, and
you may at your option offer warranty protection in exchange for a fee.

  2. You may modify your copy or copies of the Program or any portion
of it, thus forming a work based on the Program, and copy and
distribute such modifications or work under the terms of Section 1
above, provided that you also meet all of these conditions:

    a) You must cause the modified files to carry prominent notices
    stating that you changed the files and the date of any change.

    b) You must cause any work that you distribute or publish, that in
    whole or in part contains or is derived from the Program or any
    part thereof, to be licensed as a whole at no charge to all third
    parties under the terms of this License.

    c) If the modified program normally reads commands interactively
    when run, you must cause it, when started running for such
    interactive use in the most ordinary way, to print or display an
    announcement including an appropriate copyright notice and a
    notice that there is no warranty (or else, saying that you provide
    a warranty) and that users may redistribute the program under
    these conditions, and telling the user how to view a copy of this
    License.  (Exception: if the Program itself is interactive but
    does not normally print such an announcement, your work based on
    the Program is not required to print an announcement.)

These requirements apply to the modified work as a whole.  If
identifiable sections of that work are not derived from the Program,
and can be reasonably considered independent and separate works in
themselves, then this License, and its terms, do not apply to those
sections when you distribute them as separate works.  But when you
distribute the same sections as part of a whole which is a work based
on the Program, the distribution of the whole must be on the terms of
this License, whose permissions for other licensees extend to the
entire whole, and thus to each and every part regardless of who wrote it.

Thus, it is not the intent of this section to claim rights or contest
your rights to work written entirely by you; rather, the intent is to
exercise the right to control the distribution of derivative or
collective works based on the Program.

In addition, mere aggregation of another work not based on the Program
with the Program (or with a work based on the Program) on a volume of
a storage or distribution medium does not bring the other work under
the scope of this License.

  3. You may copy and distribute the Program (or a work based on it,
under Section 2) in object code or executable form under the terms of
Sections 1 and 2 above provided that you also do one of the following:

    a) Accompany it with the complete corresponding machine-readable
    source code, which must be distributed under the terms of Sections
    1 and 2 above on a medium customarily used for software interchange; or,

    b) Accompany it with a written offer, valid for at least three
    years, to give any third party, for a charge no more than your
    cost of physically performing source distribution, a complete
    machine-readable copy of the corresponding source code, to be
    distributed under the terms of Sections 1 and 2 above on a medium
    customarily used for software interchange; or,

    c) Accompany it with the information you received as to the offer
    to distribute corresponding source code.  (This alternative is
    allowed only for noncommercial distribution and only if you
    received the program in object code or executable form with such
    an offer, in accord with Subsection b above.)

The source code for a work means the preferred form of the work for
making modifications to it.  For an executable work, complete source
code means all the source code for all modules it contains, plus any
associated interface definition files, plus the scripts used to
control compilation and installation of the executable.  However, as a
special exception, the source code distributed need not include
anything that is normally distributed (in either source or binary
form) with the major components (compiler, kernel, and so on) of the
operating system on which the executable runs, unless that component
itself accompanies the executable.

If distribution of executable or object code is made by offering
access to copy from a designated place, then offering equivalent
access to copy the source code from the same place counts as
distribution of the source code, even though third parties are not
compelled to copy the source along with the object code.

  4. You may not copy, modify, sublicense, or distribute the Program
except as expressly provided under this License.  Any attempt
otherwise to copy, modify, sublicense or distribute the Program is
void, and will automatically terminate your rights under this License.
However, parties who have received copies, or rights, from you under
this License will not have their licenses terminated so long as such
parties remain in full compliance.

  5. You are not required to accept this License, since you have not
signed it.  However, nothing else grants you permission to modify or
distribute the Program or its derivative works.  These actions are
prohibited by law if you do not accept this License.  Therefore, by
modifying or distributing the Program (or any work based on the
Program), you indicate your acceptance of this License to do so, and
all its terms and conditions for copying, distributing or modifying
the Program or works based on it.

  6. Each time you redistribute the Program (or any work based on the
Program), the recipient automatically receives a license from the
original licensor to copy, distribute or modify the Program subject to
these terms and conditions.  You may not impose any further
restrictions on the recipients' exercise of the rights granted herein.
You are not responsible for enforcing compliance by third parties to
this License.

  7. If, as a consequence of a court judgment or allegation of patent
infringement or for any other reason (not limited to patent issues),
conditions are imposed on you (whether by court order, agreement or
otherwise) that contradict the conditions of this License, they do not
excuse you from the conditions of this License.  If you cannot
distribute so as to satisfy simultaneously your obligations under this
License and any other pertinent obligations, then as a consequence you
may not distribute the Program at all.  For example, if a patent
license would not permit royalty-free redistribution of the Program by
all those who receive copies directly or indirectly through you, then
the only way you could satisfy both it and this License would be to
refrain entirely from distribution of the Program.

If any portion of this section is held invalid or unenforceable under
any particular circumstance, the balance of the section is intended to
apply and the section as a whole is intended to apply in other
circumstances.

It is not the purpose of this section to induce you to infringe any
patents or other property right claims or to contest validity of any
such claims; this section has the sole purpose of protecting the
integrity of the free software distribution system, which is
implemented by public license practices.  Many people have made
generous contributions to the wide range of software distributed
through that system in reliance on consistent application of that
system; it is up to the author/donor to decide if he or she is willing
to distribute software through any other system and a licensee cannot
impose that choice.

This section is intended to make thoroughly clear what is believed to
be a consequence of the rest of this License.

  8. If the distribution and/or use of the Program is restricted in
certain countries either by patents or by copyrighted interfaces, the
original copyright holder who places the Program under this License
may add an explicit geographical distribution limitation excluding
those countries, so that distribution is permitted only in or among
countries not thus excluded.  In such case, this License incorporates
the limitation as if written in the body of this License.

  9. The Free Software Foundation may publish revised and/or new versions
of the General Public License from time to time.  Such new versions will
be similar in spirit to the present version, but may differ in detail to
address new problems or concerns.

Each version is given a distinguishing version number.  If the Program
specifies a version number of this License which applies to it and "any
later version", you have the option of following the terms and conditions
either of that version or of any later version published by the Free
Software Foundation.  If the Program does not specify a version number of
this License, you may choose any version ever published by the Free Software
Foundation.

  10. If you wish to incorporate parts of the Program into other free
programs whose distribution conditions are different, write to the author
to ask for permission.  For software which is copyrighted by the Free
Software Foundation, write to the Free Software Foundation; we sometimes
make exceptions for this.  Our decision will be guided by the two goals
of preserving the free status of all derivatives of our free software and
of promoting the sharing and reuse of software generally.

                            NO WARRANTY

  11. BECAUSE THE PROGRAM IS LICENSED FREE OF CHARGE, THERE IS NO WARRANTY
FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW.  EXCEPT WHEN
OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES
PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED
OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  THE ENTIRE RISK AS
TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU.  SHOULD THE
PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING,
REPAIR OR CORRECTION.

  12. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING
WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MAY MODIFY AND/OR
REDISTRIBUTE THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES,
INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING
OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED
TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY
YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER
PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE
POSSIBILITY OF SUCH DAMAGES.

                     END OF TERMS AND CONDITIONS

            How to Apply These Terms to Your New Programs

  If you develop a new program, and you want it to be of the greatest
possible use to the public, the best way to achieve this is to make it
free software which everyone can redistribute and change under these terms.

  To do so, attach the following notices to the program.  It is safest
to attach them to the start of each source file to most effectively
convey the exclusion of warranty; and each file should have at least
the "copyright" line and a pointer to where the full notice is found.

    <one line to give the program's name and a brief idea of what it does.>
    Copyright (C) <year>  <name of author>

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License along
    with this program; if not, write to the Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

Also add information on how to contact you by electronic and paper mail.

If the program is interactive, make it output a short notice like this
when it starts in an interactive mode:

    Gnomovision version 69, Copyright (C) year name of author
    Gnomovision comes with ABSOLUTELY NO WARRANTY; for details type `show w'.
    This is free software, and you are welcome to redistribute it
    under certain conditions; type `show c' for details.

The hypothetical commands `show w' and `show c' should show the appropriate
parts of the General Public License.  Of course, the commands you use may
be called something other than `show w' and `show c'; they could even be
mouse-clicks or menu items--whatever suits your program.

You should also get your employer (if you work as a programmer) or your
school, if any, to sign a "copyright disclaimer" for the program, if
necessary.  Here is a sample; alter the names:

  Yoyodyne, Inc., hereby disclaims all copyright interest in the program
  `Gnomovision' (which makes passes at compilers) written by James Hacker.

  <signature of Ty Coon>, 1 April 1989
  Ty Coon, President of Vice

This General Public License does not permit incorporating your program into
proprietary programs.  If your program is a subroutine library, you may
consider it more useful to permit linking proprietary applications with the
library.  If this is what you want to do, use the GNU Lesser General
Public License instead of this License.
The plugins under this directory are invoked by bzr, and are not used
directly by Review Board. They are effectively a separate source tree,
and cannot be imported under the "reviewboard" namespace.
This is a Bazaar control directory.
Do not change any files in this directory.
See http://bazaar-vcs.org/ for more information about Bazaar.
                    F̨ɏŠq-YYQ            uHello
                         L`i/'                     	
goodbye
This is a Subversion repository; use the 'svnadmin' tool to examine
it.  Do not add, delete, or modify files here unless you know how
to avoid corrupting the repository.

Visit http://subversion.tigris.org/ for more information.
We are using a custom release of CodeMirror (saved as
codemirror-5.48.2.js), built locally from a source tree.

If you make any modifications to the list of modules, or bump the version, you
must update this file!

Our build of CodeMirror is built with the following modules:

Add-ons:
  * display/placeholder.js
  * edit/continuelist.js
  * edit/matchbrackets.js
  * lint/json-lint.js
  * lint/lint.js
  * mode/overlay.js
  * mode/simple.js

Modes:
  * coffeescript.js
  * css.js
  * gfm.js
  * go.js
  * htmlmixed.js
  * javascript.js
  * jsx.js
  * perl.js
  * php.js
  * python.js
  * rst.js
  * ruby.js
  * rust.js
  * shell.js
  * sql.js
  * swift.js
  * markdown.js
  * xml.js
  * yaml.js

To build, download the CodeMirror source for the proper version and run:

cat lib/codemirror.js \
    addon/display/placeholder.js \
    addon/edit/continuelist.js \
    addon/edit/matchbrackets.js \
    addon/lint/json-lint.js \
    addon/lint/lint.js \
    addon/mode/overlay.js \
    addon/mode/simple.js \
    mode/coffeescript/coffeescript.js \
    mode/css/css.js \
    mode/gfm/gfm.js \
    mode/go/go.js \
    mode/htmlmixed/htmlmixed.js \
    mode/javascript/javascript.js \
    mode/jsx/jsx.js \
    mode/markdown/markdown.js \
    mode/perl/perl.js \
    mode/php/php.js \
    mode/python/python.js \
    mode/rst/rst.js \
    mode/ruby/ruby.js \
    mode/rust/rust.js \
    mode/shell/shell.js \
    mode/sql/sql.js \
    mode/swift/swift.js \
    mode/xml/xml.js \
    mode/yaml/yaml.js \
    > codemirror-5.48.2.js
{% load i18n%}{% autoescape off %}{% blocktrans %}You're receiving this e-mail because you requested a password reset
for your account at {{site_name}}.

Please go to the following page and choose a new password:{% endblocktrans %}
{% block reset_link %}{{protocol}}://{{domain}}{% url 'password_reset_confirm' uidb64=uid token=token %}{% endblock %}

{% blocktrans %}In case you've forgotten, your username is {{user}}{% endblocktrans %}

{% blocktrans with PRODUCT_NAME=settings.PRODUCT_NAME %}Thanks for using {{PRODUCT_NAME}}!{% endblocktrans %}

{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_utils %}
------------------------------------------
This is an automatically generated e-mail.
------------------------------------------

Hi {{user|user_displayname}},

A new API token has been added to your {{PRODUCT_NAME}} account on
{{site_url}}.

The API token ID starts with {{partial_token}} and was added
{{api_token.time_added}}.

If you did not create this token, you should revoke it at
{{api_token_url}}, change your password, and talk to your
administrator.
{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_utils %}
------------------------------------------
This is an automatically generated e-mail.
------------------------------------------

Hi {{user|user_displayname}},

One of your API tokens has been deleted from your {{PRODUCT_NAME}} account on
{{site_url}}.

The API token ID was {{api_token.token}}. Any clients
that were using this token will no longer be able to authenticate.

If you did not delete this token, you should change your password and talk
to your administrator.
{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_utils %}
------------------------------------------
This is an automatically generated e-mail.
------------------------------------------

Hi {{user|user_displayname}},

One of your API tokens has been updated on your {{PRODUCT_NAME}} account on
{{site_url}}.

The API token ID starts with {{partial_token}} and was updated
{{api_token.last_updated}}.

If you did not update this token, you should revoke it at
{{api_token_url}}, change your password, and talk to your
administrator.
{% endautoescape %}
{% autoescape off %}{% load djblets_email %}{% load djblets_utils %}
------------------------------------------
This is an automatically generated e-mail.
------------------------------------------

{{user.username}} has registered on <{{site_url}}> on {{user.date_joined}}.

If you want to grant certain permissions for this user, please visit <{{user_url}}>.
{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_utils %}
------------------------------------------
This is an automatically generated e-mail.
------------------------------------------

Hi {{user|user_displayname}},

Your password has been successfully changed on <{{server_url}}>.
If you did not change your password, please contact a server administrator
immediately.

{% if has_api_tokens %}
You currently have API tokens. Changing your password does not reset them. If
you wish to invalidate your API tokens, you must do that manually at
<{{api_token_url}}>.
{% endif %}
{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_utils markdown_email reviewtags %}

{% condense %}
{% ifnotequal reply.body_top "" %}
> On {{review.time_emailed}}, {{review.user|user_displayname}} wrote:
{{review.body_top|markdown_email_text:review.body_top_rich_text|quote_text:2}}{% for reply_review in review.public_replies %}{% ifnotequal reply_review.body_top "" %}{% ifnotequal reply_review reply %}
> 
> {{reply_review.user|user_displayname}} wrote:
{{reply_review.body_top|markdown_email_text:reply_review.body_top_rich_text|indent|quote_text}}{% endifnotequal %}{% endifnotequal %}{% endfor %}

{{reply.body_top|markdown_email_text:reply.body_top_rich_text}}
{% endifnotequal %}


{% for comment in reply.file_attachment_comments.all %}
> On {{review.time_emailed}}, {{review.user|user_displayname}} wrote:
> > File Attachment: {% if comment.file_attachment.caption %}{{comment.file_attachment.caption}} - {% endif %}{{comment.get_link_text}}
> > <{{site_url}}{{comment.get_review_url}}>
> >
{{comment.reply_to.text|markdown_email_text:comment.reply_to.rich_text|indent|quote_text:2}}{% for reply_comment in comment.reply_to.public_replies %}{%  ifnotequal comment reply_comment %}
> 
> {{reply_comment.review.get.user|user_displayname}} wrote:
{{reply_comment.text|markdown_email_text:reply_comment.rich_text|indent|quote_text}}{%  endifnotequal %}{% endfor %}

{{comment.text|markdown_email_text:comment.rich_text}}


{% endfor %}
{% for comment in reply.general_comments.all %}
> On {{review.time_emailed}}, {{review.user|user_displayname}} wrote:
> > <{{site_url}}{{comment.get_review_url}}>
> >
{{ comment.reply_to.text|markdown_email_text:comment.reply_to.rich_text|indent|quote_text:2}}{% for reply_comment in comment.reply_to.public_replies %}{%  ifnotequal comment reply_comment %}
>
> {{reply_comment.review.get.user|user_displayname}} wrote:
{{reply_comment.text|markdown_email_text:reply_comment.rich_text|indent|quote_text}}{%  endifnotequal %}{% endfor %}

{{comment.text|markdown_email_text:comment.rich_text}}


{% endfor %}
{% for comment in reply.screenshot_comments.all %}
> On {{review.time_emailed}}, {{review.user|user_displayname}} wrote:
> > Screenshot: {{ comment.screenshot.caption }}
> > <{{site_url}}{{comment.get_review_url}}>
> >
{{ comment.reply_to.text|markdown_email_text:comment.reply_to.rich_text|indent|quote_text:2}}{% for reply_comment in comment.reply_to.public_replies %}{%  ifnotequal comment reply_comment %}
> 
> {{reply_comment.review.get.user|user_displayname}} wrote:
{{reply_comment.text|markdown_email_text:reply_comment.rich_text|indent|quote_text}}{%  endifnotequal %}{% endfor %}

{{comment.text|markdown_email_text:comment.rich_text}}


{% endfor %}
{% for entry in comment_entries %}
> On {{review.time_emailed}}, {{review.user|user_displayname}} wrote:
{%  condense 1 %}
{%   definevar "lines_info" %}{% diff_comment_line_numbers entry.chunks entry.comment %}{% enddefinevar %}
> > {{entry.comment.filediff.source_file_display}}
{% if lines_info %}{{lines_info|quote_text:2}}{% endif %}
> > <{{site_url}}{{entry.comment.get_absolute_url}}>
{%  endcondense %}
> >
{{entry.comment.reply_to.text|markdown_email_text:entry.comment.reply_to.rich_text|indent|quote_text:2}}{% for reply_comment in entry.comment.reply_to.public_replies %}{%  ifnotequal entry.comment reply_comment %}
> 
> {{reply_comment.review.get.user|user_displayname}} wrote:
{{reply_comment.text|markdown_email_text:reply_comment.rich_text|indent|quote_text}}{%  endifnotequal %}{% endfor %}

{{entry.comment.text|markdown_email_text:entry.comment.rich_text}}


{% endfor %}

{% ifnotequal reply.body_bottom "" %}
On {{review.time_emailed}}, {{review_request.submitter|user_displayname}} wrote:
{{review.body_bottom|markdown_email_text:review.body_bottom_rich_text|quote_text:2}}{% for reply_review in review.public_replies %}{% ifnotequal reply_review.body_bottom "" %}{% ifnotequal reply_review reply %}
> 
> {{reply_review.user|user_displayname}} wrote:
{{reply_review.body_bottom|markdown_email_text:reply_review.body_bottom_rich_text|indent|quote_text}}{% endifnotequal %}{% endifnotequal %}{% endfor %}

{{reply.body_bottom|markdown_email_text:reply.body_bottom_rich_text}}
{% endifnotequal %}

- {% ifnotequal reply.user.first_name "" %}{{reply.user.first_name}}{% else %}{{reply.user.username}}{% endifnotequal %}
{% endcondense %}


-----------------------------------------------------------
This is an automatically generated e-mail. To reply, visit:
{{site_url}}{{review.get_absolute_url}}
-----------------------------------------------------------


On {{review_request.time_emailed}}, {{review_request.submitter|user_displayname}} wrote:
{% quoted_email "notifications/review_request_email.txt" %}
{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_extensions djblets_utils markdown_email rb_extensions reviewtags %}
-----------------------------------------------------------
This is an automatically generated e-mail. To reply, visit:
{{site_url}}{{review.get_absolute_url}}
-----------------------------------------------------------
{% if review.ship_it %}
{%  if has_issues %}
{{review.FIX_IT_THEN_SHIP_IT_TEXT}}
{%  else %}
{{review.SHIP_IT_TEXT}}
{%  endif %}
{% endif %}
{% template_hook_point "review-email-text-summary" %}
{% if review.body_top %}
{{review.body_top|markdown_email_text:review.body_top_rich_text}}
{% endif %}{% for comment in review.file_attachment_comments.all %}

File Attachment: {% if comment.file_attachment.caption %}{{comment.file_attachment.caption}} - {% endif %}{{comment.get_link_text}}
<{{site_url}}{{comment.get_review_url}}>

{% filter indent %}{% condense 2 %}
{%  comment_detail_display_hook comment "text-email" %}

{{comment.text|markdown_email_text:comment.rich_text}}
{% endcondense %}{% endfilter %}

{% endfor %}{% for comment in review.general_comments.all %}

{% filter indent %}{% condense 2 %}
{%  comment_detail_display_hook comment "text-email" %}

{{comment.text|markdown_email_text:comment.rich_text}}
{% endcondense %}{% endfilter %}

{% endfor %}{% for comment in review.screenshot_comments.all %}

Screenshot: {{ comment.screenshot.caption }}
<{{site_url}}{{comment.get_review_url}}>

{% filter indent %}{% condense 2 %}
{%  comment_detail_display_hook comment "text-email" %}

{{comment.text|markdown_email_text:comment.rich_text}}
{% endcondense %}{% endfilter %}

{% endfor %}{% for entry in comment_entries %}

{% condense 1 %}
{{entry.comment.filediff.source_file_display}}
{% diff_comment_line_numbers entry.chunks entry.comment %}
<{{site_url}}{{entry.comment.get_review_url}}>
{% endcondense %}

{% filter indent %}{% condense 2 %}
{%  comment_detail_display_hook entry.comment "text-email" %}

{{entry.comment.text|markdown_email_text:entry.comment.rich_text}}
{% endcondense %}{% endfilter %}

{% endfor %}{% if review.body_bottom %}
{{review.body_bottom|markdown_email_text:review.body_bottom_rich_text}}
{% endif %}
- {{review.user|user_displayname}}


On {{review_request.time_emailed}}, {{review_request.submitter|user_displayname}} wrote:
{% quoted_email "notifications/review_request_email.txt" %}
{% endautoescape %}
{% autoescape off %}{% load djblets_email djblets_utils markdown_email reviewtags %}
-----------------------------------------------------------
This is an automatically generated e-mail. To reply, visit:
{{site_url}}{{review_request.get_absolute_url}}
-----------------------------------------------------------

{% condense %}
{% if review_request.email_message_id %}
(Updated {{review_request.time_emailed}})

{% endif %}
{% if changes and changes.status and review_request.status in "SD" %}Status
------
{%  if review_request.status == 'S' %}
This change has been marked as submitted.
{%  elif review_request.status == 'D' %}
This change has been discarded.
{%  endif %}
{% endif %}

Review request for {% reviewer_list review_request %}.

{% if change_text %}
Changes
-------

{{change_text|markdown_email_text:change_rich_text}}
{% endif %}

{% if changes %}{% if changes.summary %}Summary (updated)
-----------------

{{review_request.summary}}
{% endif %}{% endif %}

Description{% if changes %}{% if changes.description %} (updated){% endif %}{% endif %}
-------

{{review_request.description|markdown_email_text:review_request.description_rich_text}}


{% with review_request.get_latest_diffset as latest_diffset %}
{%  if latest_diffset %}
Diffs{% if changes and changes.diff %} (updated){% endif %}
-----
{%   for filediff in latest_diffset.files.all %}
  {{ filediff.source_file_display }} {{ filediff.source_revision }} {% endfor %}

{%   with latest_diffset.revision as rev %}
Diff: {{site_url}}{% url 'view-diff-revision' review_request.display_id rev %}
{%    if rev > 1 and changes and changes.diff %}
Changes: {{site_url}}{% url 'view-interdiff' review_request.display_id rev|add:"-1" rev %}
{%    endif %}
{%   endwith %}
{%  endif %}
{% endwith %}


Testing{% if changes and changes.testing_done %} (updated){% endif %}
-------

{{review_request.testing_done|markdown_email_text:review_request.testing_done_rich_text}}
{% if review_request.file_attachments.count %}

File Attachments{% if changes and changes.files %} (updated){% endif %}
----------------
{% for file in review_request.file_attachments.all %}
{{file.caption}}
  {{file.get_absolute_url}}{% endfor %}

{% endif %}
{% if review_request.screenshots.count %}

Screenshots{% if changes and changes.screenshots %} (updated){% endif %}
-----------
{% for screenshot in review_request.screenshots.all %}
{{ screenshot.caption }}
  {{site_url}}{{ screenshot.get_absolute_url }}{% endfor %}

{% endif %}
{% if review_request.bugs_closed %}

Bugs: {{review_request.get_bug_list|humanize_list}}{% if review_request.repository and review_request.repository.bug_tracker %}{% for bug in review_request.get_bug_list %}
    {{bug|bug_url:review_request}}{% endfor %}
{% endif %}
{% endif %}

{% condense 0%}
{% if review_request.repository %}
Repository: {{review_request.repository.name}}
{% endif %}
{% endcondense %}
{% condense 0%}
{% if review_request.branch %}
  Branch: {{review_request.branch}}
{% endif %}
{% endcondense %}

Thanks,

{{ review_request.submitter|user_displayname }}
{% endcondense %}
{% endautoescape %}
{# Haystack data template for UserIndex #}
{{object.username}}
{% if not object.get_profile.is_private %}
{{object.email}}
{{object.get_full_name}}
{% endif %}
{# Haystack data template for ReviewRequestIndex #}
{{object.display_id}}
{{object.summary}}
{{object.description}}
{{object.testing_done}}
{{object.bugs_closed}}
{{object.submitter.username}}
{% if not object.submitter.get_profile.is_private %}{{object.submitter.get_full_name}}{% endif %}
{{object.get_all_diff_filenames}}
{{object.commit_id}}

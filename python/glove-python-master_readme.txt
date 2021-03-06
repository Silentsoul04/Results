# Changelog

## [0.1.0][2016-01-11]
### Changed
- add algorithm tests for corpus construction and model fitting
- remove dependency on Cython for intallation, the required .c and .cpp files are now included
- use py.test for testing
- removed dependency on C++11 features by using a different sparse matrix structure for corpus construction
- faster coocurrence matrix construction

### Removed
- max_map_size argument removed from Corpus.fit

                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   APPENDIX: How to apply the Apache License to your work.

      To apply the Apache License to your work, attach the following
      boilerplate notice, with the fields enclosed by brackets "[]"
      replaced with your own identifying information. (Don't include
      the brackets!)  The text should be enclosed in the appropriate
      comment syntax for the file format. We also recommend that a
      file or class name and description of purpose be included on the
      same "printed page" as the copyright notice for easier
      identification within third-party archives.

   Copyright 2014 Maciej Kula

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.# glove-python

[![Circle CI](https://circleci.com/gh/maciejkula/glove-python.svg?style=svg)](https://circleci.com/gh/maciejkula/glove-python)

A toy python implementation of [GloVe](http://www-nlp.stanford.edu/projects/glove/).

Glove produces dense vector embeddings of words, where words that occur together are close in the resulting vector space.

While this produces embeddings which are similar to [word2vec](https://code.google.com/p/word2vec/) (which has a great python implementation in [gensim](http://radimrehurek.com/gensim/models/word2vec.html)), the method is different: GloVe produces embeddings by factorizing the logarithm of the corpus word co-occurrence matrix.

The code uses asynchronous stochastic gradient descent, and is implemented in Cython. Most likely, it contains a tremendous amount of bugs.

## Installation
Install from pypi using pip: `pip install glove_python`.

Note for OSX users: due to its use of OpenMP, glove-python does not compile under Clang. To install it, you will need a reasonably recent version of `gcc` (from Homebrew for instance). This should be picked up by `setup.py`; if it is not, please open an issue.

Building with the default Python distribution included in OSX is also not supported; please try the version from Homebrew or Anaconda.

## Usage
Producing the embeddings is a two-step process: creating a co-occurrence matrix from the corpus, and then using it to produce the embeddings. The `Corpus` class helps in constructing a corpus from an interable of tokens; the `Glove` class trains the embeddings (with a sklearn-esque API).

There is also support for rudimentary pagragraph vectors. A paragraph vector (in this case) is an embedding of a paragraph (a multi-word piece of text) in the word vector space in such a way that the paragraph representation is close to the words it contains, adjusted for the frequency of words in the corpus (in a manner similar to tf-idf weighting). These can be obtained after having trained word embeddings by calling the `transform_paragraph` method on the trained model.

## Examples
`example.py` has some example code for running simple training scripts: `ipython -i -- examples/example.py -c my_corpus.txt -t 10` should process your corpus, run 10 training epochs of GloVe, and drop you into an `ipython` shell where `glove.most_similar('physics')` should produce a list of similar words.

If you want to process a wikipedia corpus, you can pass file from [here](http://dumps.wikimedia.org/enwiki/latest/) into the `example.py` script using the `-w` flag. Running `make all-wiki` should download a small wikipedia dump file, process it, and train the embeddings. Building the cooccurrence matrix will take some time; training the vectors can be speeded up by increasing the training parallelism to match the number of physical CPU cores available.

Running this on my machine yields roughly the following results:

```
In [1]: glove.most_similar('physics')
Out[1]:
[('biology', 0.89425889335342257),
 ('chemistry', 0.88913708236100086),
 ('quantum', 0.88859617025616333),
 ('mechanics', 0.88821824562025431)]

In [4]: glove.most_similar('north')
Out[4]:
[('west', 0.99047203572917908),
 ('south', 0.98655786905501008),
 ('east', 0.97914140138065575),
 ('coast', 0.97680427897282185)]

In [6]: glove.most_similar('queen')
Out[6]:
[('anne', 0.88284931171714842),
 ('mary', 0.87615260138308615),
 ('elizabeth', 0.87362497374226267),
 ('prince', 0.87011034923161801)]

In [19]: glove.most_similar('car')
Out[19]:
[('race', 0.89549347066796814),
 ('driver', 0.89350343749207217),
 ('cars', 0.83601334715106568),
 ('racing', 0.83157724991920212)]
```

## Development
Pull requests are welcome.

When making changes to the `.pyx` extension files, you'll need to run `python setup.py cythonize` in order to produce the extension `.c` and `.cpp` files before running `pip install -e .`.
<user> 0.62415 0.62476 -0.082335 0.20101 -0.13741 -0.11431 0.77909 2.6356 -0.46351 0.57465 -0.024888 -0.015466 -2.9696 -0.49876 0.095034 -0.94879 -0.017336 -0.86349 -1.3348 0.046811 0.36999 -0.57663 -0.48469 0.40078 0.75345
. 0.69586 -1.1469 -0.41797 -0.022311 -0.023801 0.82358 1.2228 1.741 -0.90979 1.3725 0.1153 -0.63906 -3.2252 0.61269 0.33544 -0.57058 -0.50861 -0.16575 -0.98153 -0.8213 0.24333 -0.14482 -0.67877 0.7061 0.40833
: 1.1242 0.054519 -0.037362 0.10046 0.11923 -0.30009 1.0938 2.537 -0.072802 1.0491 1.0931 0.066084 -2.7036 -0.14391 -0.22031 -0.99347 -0.65072 -0.030948 -1.0817 -0.64701 0.32341 -0.41612 -0.5268 -0.047166 0.71549
rt 0.74056 0.9155 -0.16352 0.35843 0.05266 0.1456 1.0421 2.8073 0.12865 1.0492 0.13033 0.20508 -2.6686 -0.50551 -0.29574 -0.91433 -0.40456 -1.0988 -1.0333 -0.17875 0.37979 -0.25922 -0.74854 0.36001 0.61206
, 0.84705 -1.0349 -0.050419 0.27164 -0.58659 0.99514 0.25267 1.6963 0.10313 0.80073 0.74655 -1.2667 -4.036 -0.22557 0.16322 -0.67015 -0.64812 0.010373 -0.71889 -0.74997 0.24862 0.10319 -1.1732 0.58196 0.33846
<repeat> 0.67867 -0.74651 -0.31831 -0.093681 0.062057 0.77956 1.5604 2.0332 -0.95379 1.2358 -0.081705 -0.42269 -2.5273 0.51772 0.29574 -0.76079 -0.57992 -0.51783 -1.1715 -0.53952 0.36752 -0.2758 -0.086496 1.0115 0.56436
<hashtag> 0.18227 -0.29194 -1.3632 -1.201 0.084332 0.018943 1.3408 2.3866 -1.2761 0.39897 -0.16731 -0.52372 -3.5758 -0.25648 -0.5531 -0.62011 -0.71249 -0.12025 -0.91766 0.65635 -0.55258 -1.1655 0.10899 -1.6099 1.6189
<number> 1.3956 0.2892 0.48572 -1.1412 0.21461 1.0714 0.25408 2.1181 0.30252 0.75955 1.1299 -0.021373 -3.7757 0.89387 -0.71476 -1.6997 -0.42166 -0.12601 -1.2984 0.41689 -0.84993 -1.5199 0.40681 0.15024 0.26997
<url> 0.80384 -1.0366 -0.53877 -1.0806 0.84718 -0.36196 1.0065 1.3067 -0.61225 0.30781 0.46974 -0.23264 -3.3882 -0.46778 -0.55105 -1.6926 -0.78708 0.28378 -0.73638 0.10216 -0.18703 -2.133 -0.17787 -0.97788 1.394
! 0.4049 -0.87651 -0.23362 -0.34844 -0.097002 0.40895 1.6928 1.7058 -1.293 0.70091 -0.12498 -0.75998 -3.1586 0.14081 0.57255 -0.46097 -0.75721 -0.72414 -1.4071 -0.17224 0.0099324 -0.45711 0.074886 1.2035 1.1614
i -0.26079 0.59108 0.61622 -0.70368 -0.85159 -0.23238 1.0481 0.066642 -0.54907 0.70047 -0.87221 -0.013954 -5.9671 -0.43106 -0.9154 0.53744 0.57099 -0.27181 -0.84178 -0.59682 0.4516 0.34097 0.076869 0.2284 0.2758
a 0.21294 0.31035 0.17694 0.87498 0.067926 0.59171 -0.098218 1.5896 -0.428 -1.3655 -0.15278 -2.501 -5.5652 -0.10232 0.39577 0.1555 -0.55181 0.34671 -0.57379 -0.30717 0.043623 -0.39707 0.64551 -0.33537 0.020467
" 1.0822 -0.59378 -0.19992 0.66626 0.18051 0.014404 1.4227 2.3584 -0.2701 1.4194 0.61099 -0.29541 -2.8885 -0.070205 -0.038122 -0.50855 -0.4445 0.076176 -0.96879 -0.57778 0.39206 0.20976 -0.73835 0.031611 0.72533
the -0.010167 0.020194 0.21473 0.17289 -0.43659 -0.14687 1.8429 -0.15753 0.18187 -0.31782 0.06839 0.51776 -6.3371 0.48066 0.13777 -0.48568 0.39 -0.0019506 -0.10218 0.21262 -0.86146 0.17263 0.18783 -0.8425 -0.31208
? 1.104 -0.34629 0.088792 -0.2554 -0.023462 0.51487 0.7491 1.7858 0.16928 0.93679 0.010994 -0.98983 -3.7061 -0.82598 0.90447 -0.41301 -0.617 -0.62424 -1.1698 -0.022587 0.26791 -0.076523 -1.1142 1.336 0.20145
you -0.41586 0.32548 -0.087621 0.2018 -0.80017 -0.34418 2.1431 0.37188 -0.9409 0.24283 -0.86396 0.63858 -6.0171 -0.54081 -0.43305 0.095707 0.37971 -1.1432 0.11382 -0.38361 0.41758 0.081476 -0.02659 0.75438 -0.77178
to 0.28228 0.019558 0.11509 -0.39242 -1.0503 -0.54278 1.1357 -0.34251 0.80636 -0.47359 -0.77194 -0.73689 -6.2619 -0.34902 -0.35532 -0.60148 -0.054534 -0.67057 -0.39972 -1.324 -0.43765 0.30045 0.2143 0.25422 -0.26674
( 0.026645 -0.15996 -0.13042 0.32999 0.24416 0.41042 1.3001 2.6126 0.70933 0.91401 0.21455 0.2219 -2.6304 -0.11566 -0.32597 -2.167 -1.0084 0.43317 -0.85766 -0.20587 -0.037961 -1.5767 0.15105 0.24585 1.1149
<allcaps> 0.82488 -0.3125 -1.2156 -1.0703 -0.26568 -0.2475 2.1968 2.179 -0.37712 1.3096 0.51299 0.68645 -2.0813 -0.052276 -0.4715 -1.7417 -1.3162 -0.32637 -0.78276 0.50433 0.078971 -2.1496 0.63889 -0.57727 1.4871
<elong> 0.23809 -0.09146 0.15923 -0.018792 0.12084 0.68245 1.3484 2.7759 -0.78706 0.85131 -0.95748 -0.34804 -2.0028 -0.51581 0.15512 -1.2631 -0.48455 -1.1553 -1.7698 0.39001 0.76965 0.24155 0.84985 2.0607 0.85529
) 0.34127 -0.43348 -0.35918 -0.15297 -0.078167 0.064745 1.3919 2.2717 0.53841 1.2455 0.65984 0.549 -2.6548 0.00082321 -0.38957 -1.952 -1.1767 0.2034 -0.91539 0.09037 0.16488 -1.8562 0.13423 0.57839 1.074
me 0.58866 0.0060408 -0.22022 1.0119 -0.7583 0.12081 -0.025355 1.596 -1.521 -1.1867 -0.42468 -2.0128 -5.3977 -1.2343 0.17889 1.3491 -0.011538 -0.063358 -0.18676 -0.18863 0.81819 -0.33465 1.6392 1.4183 0.16919
de 1.423 -0.46838 -0.16331 1.2443 1.0157 1.1604 -2.0031 2.5195 -0.47779 -1.8382 0.32809 -3.2301 -3.0671 -0.2536 0.87798 0.3083 -0.88685 1.2904 -1.3443 1.1462 -0.026837 -0.449 -0.006978 -0.73663 1.6404
<smile> 0.15671 -0.024377 -0.04252 -0.22052 -0.21045 -0.15969 0.70284 2.2709 -0.91873 1.5789 -0.25527 -0.63909 -2.944 -0.042341 0.12256 -1.0834 0.44036 -0.60795 -1.611 0.40592 -0.37838 -0.1601 -1.0792 1.8263 0.55963
！ 0.98004 0.38132 0.29754 -0.30478 0.40033 0.31853 1.8654 0.48166 0.56297 -0.82152 -1.2386 1.4854 -1.7059 0.093414 -2.4631 -1.365 -0.85534 0.20354 0.14737 2.1994 0.1779 -2.8695 2.1895 1.6762 2.3846
que 1.8163 -0.9435 -0.6624 1.0099 0.031072 0.33463 -0.95627 2.9703 -0.54155 -2.4489 0.29555 -3.9631 -2.5559 -0.5695 1.0982 0.73903 -1.1868 0.5865 -0.45852 0.49212 0.87361 0.14368 0.64574 0.86255 0.4955
and -0.81216 -0.28605 0.062502 -0.036869 -0.61118 -0.15568 1.625 -0.42602 0.1973 -0.19418 0.53267 0.64592 -6.1336 -0.3309 -0.0017279 -0.15173 0.20383 -0.77496 0.17629 -0.10884 -0.31234 0.2401 -0.36097 -0.049996 -0.7247
。 0.97257 1.2053 0.65594 0.7481 0.21479 0.030439 0.92262 1.9799 0.13767 -0.13729 -1.0628 1.475 -2.2513 0.92853 -2.5643 -1.6855 0.41263 1.0644 1.5803 1.2377 -0.13871 -3.2106 0.84125 0.18398 1.9644
- 0.7717 -1.0602 -0.34383 -0.09264 0.031247 0.10274 1.1822 2.0774 0.20992 0.88188 0.65696 0.041836 -3.3736 -0.71065 0.041693 -1.535 -0.55627 0.64587 -0.7243 -0.399 -0.31172 -0.58834 -0.11027 -0.067876 1.0723
my -0.74175 0.54942 0.6749 0.67924 0.13115 -0.2858 1.9227 0.11975 -0.62351 0.39304 -0.87884 0.39575 -5.9879 -0.49659 -0.26535 -0.04049 1.1247 -0.75211 -0.38015 0.49567 -0.53343 0.056762 0.69697 0.53384 -0.70807
no 1.2722 0.22154 0.1395 0.50897 0.11663 0.10291 0.21448 2.2064 -0.5623 -1.0633 0.039293 -2.9371 -4.5097 -0.51896 1.0116 0.14003 -0.32955 0.076449 1.1712 -0.66266 0.53255 0.072198 1.184 0.95736 0.20746
、 0.85424 0.25535 0.80356 -0.043311 -0.062442 0.71904 0.91777 1.8196 0.93903 -0.041324 -0.27476 2.223 -1.9891 0.60383 -3.2757 -1.4099 1.3996 1.067 0.26134 1.3922 1.2872 -2.578 0.86285 0.53713 2.3683
is -0.12532 -0.20207 -0.12672 -0.57474 -0.30313 -0.029884 1.1792 -0.1491 -0.71315 -0.12112 0.40652 1.4784 -5.995 -0.21617 0.47806 0.43448 0.13489 0.88961 -0.56926 0.33094 0.13661 0.65844 -0.41766 0.25164 -0.055809
it 0.16758 0.21434 -0.093086 0.16379 -0.60001 -0.037103 1.8577 -0.24306 -0.44864 0.28734 -0.43609 1.0839 -6.0385 -0.14872 0.31843 0.08263 0.47562 -0.5009 -0.099384 -0.18034 -0.10614 0.15238 0.32532 0.73795 -0.40859
… 0.84691 -0.27254 -0.46382 0.4686 0.77397 0.95429 0.566 2.0054 -0.79725 0.46677 -0.5743 0.55761 -2.5497 0.78614 -0.58253 -1.1329 -0.60002 0.10997 -0.66984 -0.43048 1.2045 -1.8733 0.27826 0.24504 0.83927
in -0.32929 -0.16037 0.10785 -0.3961 -0.48827 -0.17528 0.23056 -0.49115 -0.065798 0.84382 0.38091 0.46377 -5.9545 0.57595 -0.18242 0.36494 -0.0042541 0.96687 -1.5674 -0.40454 -0.79557 -0.0050535 0.021972 -0.73638 0.65277
n 0.53229 -0.30423 -0.6065 -0.15941 0.52165 -0.065076 1.3758 2.4098 -1.033 0.73698 -0.40591 -0.18263 -2.7087 0.28421 -1.8023 -1.4446 -1.4078 -0.20802 -0.94007 -0.10846 0.047255 -0.85601 0.94209 0.34083 0.66958
for -0.21749 0.45183 -0.23211 -0.27781 -0.067977 -0.63951 1.1218 -0.37536 0.18676 -0.50864 0.016423 -0.13329 -5.903 0.14596 -0.067031 -0.66199 -0.17362 -0.87281 -0.49771 -0.55289 -1.0515 -0.18484 -0.30848 -0.04478 -0.24358
/ 0.26362 -0.5406 -0.30588 -0.42799 0.4699 0.95839 1.316 2.1394 0.33286 0.44204 0.82635 0.40852 -3.0257 -0.57578 -0.6385 -1.4769 -0.94778 0.17089 -0.98404 -0.36094 -0.32045 -0.99178 0.47383 0.49367 0.86134
of 0.32543 -0.089637 -0.14733 0.4285 -0.092613 -0.17938 1.2835 -0.59714 -0.28134 -0.048954 0.54827 0.6941 -6.12 0.6724 0.018078 -0.24165 0.50342 0.65325 -0.20674 0.27639 -0.79097 0.10432 -0.6175 -0.54592 -0.069893
la 0.14261 -0.2807 -0.1258 0.45119 0.17715 0.919 -1.0333 3.8694 0.41688 -0.67503 -0.020023 -3.0843 -2.9433 0.81947 1.6001 1.7433 0.21815 0.88131 -0.97446 1.3757 1.0597 -1.1426 0.29684 -0.84936 -0.012225
's -0.21143 -0.16532 0.42022 -0.28705 -0.20637 -0.3565 1.3455 0.21057 -0.14089 -0.66701 0.54621 0.62353 -5.8742 -0.2406 0.19936 -0.61046 0.034438 0.23217 -0.66933 0.28861 0.2833 0.37067 -0.092633 -0.092978 -0.30293
* -0.0010152 -0.39872 0.18076 0.65818 -0.27114 0.15688 1.7757 2.4463 0.10599 1.254 0.11974 -0.057964 -2.2856 -1.187 -0.99771 -0.43614 -0.71053 -0.26881 -1.1703 -0.23262 -0.16339 -0.48445 0.84881 1.7162 0.76949
do 1.6477 0.12903 0.76911 -0.030854 0.27506 -0.49298 0.8206 -0.12559 0.57068 -0.79898 -1.6912 -1.7656 -5.3186 -1.2511 -0.73013 -0.90697 -1.0932 -0.53634 0.17967 -1.6247 -0.0029176 1.3184 0.45594 0.3682 0.87591
n't 0.31872 0.52105 -0.056364 -0.34805 -0.77221 -0.28169 2.06 -0.56607 -0.32574 0.073742 -0.46097 0.54654 -6.0364 -0.56174 -0.084994 0.34263 0.1017 -0.82377 0.14404 -0.73248 0.63707 0.82175 0.53894 0.3674 -0.25653
that 0.20823 0.22476 -0.070949 0.23917 -0.36076 -0.23443 1.8633 -0.4573 -0.40894 -0.055079 -0.11599 1.0568 -6.2614 -0.24912 0.37123 0.21891 0.67926 -0.35585 0.18441 -0.11821 0.58806 0.59916 0.40883 0.15874 -0.55338
on 0.21228 -0.2435 -0.57013 0.33778 -0.86072 -0.1771 0.86891 -0.11103 0.53467 -0.0036497 0.11068 0.44655 -5.6486 -0.033026 0.36245 0.74407 -0.16614 -0.61851 -1.8327 0.51321 -0.31933 -0.68438 0.59145 -0.55647 -0.31049
y 0.21767 0.19018 -0.27414 0.69654 0.12748 0.83719 -1.2804 3.8718 -0.96223 -1.1195 0.985 -2.4167 -2.9994 0.017624 1.3301 0.48203 -0.19386 0.09823 1.2263 0.80212 0.48846 -0.98181 0.53096 0.4342 0.67874
' 0.44205 -0.67697 -0.079938 0.89579 -0.043245 0.35863 0.51735 1.433 -0.21658 0.93923 0.36207 -0.27295 -3.4128 0.46583 -0.87769 -0.42464 -1.3648 0.43996 -2.4477 -0.23733 0.42426 0.18637 -0.19753 0.26109 0.44809
e 1.2775 -0.29531 0.57591 -0.42937 0.12591 -0.81734 -0.70924 1.6399 0.52233 -0.53468 -0.85909 -2.6308 -3.5076 -0.60357 -1.8392 -0.43235 -2.3822 0.14332 -1.2133 -0.33507 -0.75788 0.58005 0.38244 0.29998 0.66194
o 1.3635 0.04007 0.82928 1.0005 0.51972 0.067199 -0.39481 1.9431 0.050642 -0.139 -0.67126 -2.5206 -3.1961 -0.67686 -0.75984 -1.5995 -1.178 -0.014596 -0.88455 -0.48474 0.21677 0.41828 0.24096 0.83342 1.1436
u 0.4532 0.95597 -0.15188 -0.76201 -0.44016 0.031701 0.28219 1.9646 -0.64687 0.48962 -1.0939 0.0013035 -4.7503 0.14003 -1.4439 -0.0030859 -0.47395 -0.51914 -0.5441 0.48264 -0.076634 -0.064356 0.14666 0.48416 0.11541
en 0.69564 -0.48183 -0.080013 0.33814 0.37114 1.3014 -2.2778 2.8792 -1.5228 -0.8133 1.0348 -2.0311 -2.8536 0.61582 1.254 1.0985 0.46716 1.5167 -1.086 0.94948 0.401 -1.4937 0.25163 -0.9494 1.5508
this -0.17895 0.38406 0.073035 -0.32363 -0.092441 -0.40767 2.1 -0.11363 -0.58784 -0.17034 -0.6433 0.72388 -5.7839 -0.10406 0.52152 -0.11314 0.59554 -0.47587 -0.4551 0.084431 -0.4582 -0.16727 0.54594 0.035478 -0.16073
el 0.11335 0.59796 0.38876 0.83878 0.83717 0.24276 -1.4375 4.2874 -0.51924 -1.0783 1.0522 -2.5613 -2.5292 0.47829 2.1483 0.013401 0.58133 0.6934 0.296 -0.012265 0.37054 -0.71858 1.6555 -0.60154 0.86965
so 0.39543 -0.60706 0.34448 -0.93783 -0.30466 0.46151 1.5214 0.070674 -0.36075 0.029852 -1.1005 -0.053799 -5.079 -0.73424 -0.40314 -0.10083 -0.0022164 -0.47121 -0.88651 -1.1737 0.22514 0.87842 -0.10534 1.27 -0.22951
be -0.3435 1.0138 -0.039231 -0.61739 -0.13 0.65973 1.1861 -0.117 -0.61421 0.39945 -0.33834 0.54643 -5.4199 0.31714 -0.62972 -0.49683 0.38104 -0.52959 -0.51274 -0.88274 0.524 1.032 -0.62416 0.12028 -0.10696
'm -0.60745 0.40046 0.72375 -0.51941 -0.60935 0.49649 1.7686 -0.48596 -0.35951 0.68387 -0.94178 0.2865 -5.0159 -0.46631 -0.36731 -0.46284 0.48544 -0.32663 -0.82502 -0.88353 0.89693 0.12028 0.030383 -0.043274 0.64118
with -0.9476 0.32533 0.23967 0.29609 -0.098118 -0.10892 1.3503 -0.014157 0.15739 0.13604 -0.06848 0.68701 -5.6666 -0.41398 0.22936 -0.3325 0.49592 -0.74203 -0.032459 0.40253 -1.0907 -0.11469 -0.25527 -0.40069 -0.47669
just -0.35518 0.4803 0.49681 -0.76379 -0.64588 0.083208 1.7889 -0.3547 -0.4497 0.022174 0.18026 0.81539 -5.7024 -0.75963 -0.066477 0.52203 0.50433 -0.42471 -0.37414 -0.67191 0.48804 0.43652 0.29954 0.43855 -0.40954
> 0.67403 -0.1364 -0.080726 -0.89577 0.33463 0.21482 1.0867 2.0046 -0.61399 0.25588 -0.36965 -0.28485 -3.3158 -0.092295 -1.1617 -0.87728 -1.5146 -0.65678 -1.0679 0.61796 -0.61208 -0.614 0.39864 0.41253 0.56256
your -0.48666 0.32014 -0.27703 1.0928 0.45773 -0.37923 1.9602 -0.35099 -0.34286 0.26806 -0.49852 0.34517 -6.0877 -0.18907 -0.45247 0.026142 0.56855 -0.64653 0.21283 -0.15051 -0.59593 -0.31407 0.2869 0.27501 -1.4474
^ 0.039588 -0.11419 -0.076219 -0.12791 -0.33003 0.43771 1.8312 1.9416 -0.86341 0.62057 -0.56913 0.3571 -1.7911 -0.40879 -0.53269 -1.4991 -1.053 -0.7939 -1.8975 0.5277 -0.37142 -1.7164 -0.055501 1.9065 0.92442
like 0.068004 0.10737 0.61292 0.35446 -0.28576 0.44095 1.7574 -0.0079057 -0.66561 0.20433 -0.51421 0.46797 -5.349 -0.99746 -0.12069 0.11433 0.37355 -0.97219 -0.089747 -0.14982 0.34141 0.58987 0.51226 -0.06509 -0.068817
have -0.058224 0.79651 -0.060888 -0.58459 -0.56228 -0.072496 1.8592 -0.42394 -0.56051 -0.057096 0.44406 0.31399 -5.8856 0.061965 -0.20702 -0.046447 0.75287 -0.58468 0.25053 -0.72399 -0.13122 0.37822 -0.17631 0.43037 -0.45315
te 0.81979 -0.44008 -1.1408 1.1369 -0.71241 0.030568 -1.3383 2.9954 -1.413 -1.1037 0.57031 -2.9081 -2.3991 -1.1408 -0.15021 1.0955 -0.38832 0.88401 -0.92539 0.41138 0.77758 -0.91392 1.165 1.9987 0.51215
at -1.0206 -0.12834 1.0937 -0.74474 -0.51548 -0.50633 1.0489 -0.18161 0.86851 0.38252 -0.34213 -0.079467 -4.9305 0.91787 0.046519 -0.83393 0.77692 -0.70471 -0.99819 -0.73907 -0.57397 -0.2561 -0.24104 -0.58805 0.48638
？ 0.62413 0.77774 0.50666 -1.0425 0.69918 0.72191 0.91422 1.2456 0.21374 0.56368 -2.2575 2.2898 -1.8461 -0.57553 -2.3108 -1.4953 -0.80619 1.9734 -0.28921 2.0816 1.9227 -2.8119 0.46788 0.94142 0.99366
love -0.62645 -0.082389 0.070538 0.5782 -0.87199 -0.14816 2.2315 0.98573 -1.3154 -0.34921 -0.8847 0.14585 -4.97 -0.73369 -0.94359 0.035859 -0.026733 -0.77538 -0.30014 0.48853 -0.16678 -0.016651 -0.53164 0.64236 -0.10922
se 1.5771 -0.89176 -0.62529 0.42748 -0.83033 -0.064147 -1.6374 3.2134 0.12522 -1.2291 0.33955 -3.5723 -2.9215 -0.14489 0.10353 1.2451 -1.1518 0.27602 -0.26116 0.098035 0.73908 0.092399 0.80997 0.44311 0.62663
are 0.1866 -0.098326 -0.12268 -0.93822 -0.40161 0.6383 1.6686 -0.68036 -0.98359 -0.079512 0.38078 0.039076 -5.4147 0.02829 -0.47007 0.11377 -0.52725 -0.79312 0.58203 -0.61829 0.37025 0.2261 -0.73014 -0.1019 -0.21382
< 0.58806 -0.15251 -0.064951 -0.88166 0.15004 -0.19889 1.1618 2.0507 -0.91723 0.38324 -0.60172 0.085248 -3.0157 0.3511 -1.1353 -0.77262 -1.6993 -0.61297 -1.0837 0.67306 -0.41953 -0.76792 0.64669 0.56938 0.53808
m 0.46768 0.24442 -0.79763 -0.74 -0.41127 0.26882 -0.21232 2.257 -0.3162 -0.17906 -0.15279 -0.50826 -4.0466 0.57889 -1.1724 0.031238 -1.1387 0.039347 -1.32 1.2395 -0.56249 -1.0717 0.5102 -0.021507 0.24223
r 0.55525 0.71333 -0.49285 -0.90042 0.043085 0.11183 0.11446 2.2269 -0.69619 0.064417 -0.39974 -0.43526 -3.9523 0.35152 -1.7713 -0.77199 -1.4343 -0.39785 -0.72236 0.86474 -0.18005 -0.72005 0.44048 -0.36406 0.3805
if 0.18243 0.70534 -0.34209 -0.10779 -0.72721 -0.58802 1.7457 -0.13666 -0.61576 0.15336 -0.19019 0.70282 -5.725 -0.20901 -0.33692 0.16916 0.35872 -0.9871 0.45495 -0.36607 0.62973 0.11066 0.31315 0.08787 -0.88679
all -0.18232 0.96997 0.32174 -0.074793 -0.11618 0.095187 1.4986 -0.41357 -0.86298 0.42067 -0.53125 0.10797 -5.56 0.25913 -0.58389 0.12241 -0.15168 -0.71983 -0.16605 -0.092514 -0.34099 0.12464 0.086193 -0.1411 -0.18656
b 0.50344 0.61831 -0.24684 -0.93508 -0.11275 0.22688 0.15222 2.3432 -0.24032 0.12045 -0.60827 -0.25307 -4.0088 0.42389 -1.2794 -0.72646 -1.152 -0.36694 -0.77069 0.80603 -0.52068 -0.40503 0.23572 0.12789 0.21919
・ 1.4696 -1.1562 -1.2549 -0.045791 0.26885 1.3117 0.093971 2.056 1.8101 -0.78516 -1.127 2.8487 -2.1782 0.14884 -2.6502 -1.9661 -0.32747 1.1759 0.82536 1.7901 0.36039 -2.2292 1.1782 -0.17536 1.0635
not 0.35377 0.32604 -0.22682 -0.32412 -0.18555 0.1486 1.3914 -0.65154 -0.38197 0.17129 -0.43405 0.39154 -5.7918 -0.20201 -0.23216 -0.10638 0.070835 -0.2146 -0.094385 -1.0851 0.61683 0.82184 -0.35102 0.19177 -0.43818
but 0.17129 -0.012287 -0.32958 -0.16519 -0.54661 0.17683 1.7577 -0.63738 -0.47622 0.13892 -0.43254 0.789 -5.7212 0.068779 0.37439 0.51778 0.331 -0.74517 -0.20935 -0.21567 0.66493 0.52874 0.1066 0.47777 -0.48408
we 0.49653 1.1435 -0.28609 -0.63378 -1.2347 -0.096415 0.81466 0.31406 -0.81064 0.43028 -0.10844 0.23407 -5.5359 0.045617 -0.15732 0.74855 0.35315 -0.11169 -0.12048 -0.13965 -0.27711 0.34342 -0.40377 0.61924 0.5394
es 0.074369 -0.84513 -1.1513 0.2921 0.88949 0.8157 -0.71079 3.9407 -0.90175 -0.99754 1.1565 -2.4328 -1.9748 -0.28035 1.8613 0.84797 -0.055742 0.95519 -0.066362 -0.10171 1.2204 -0.12053 0.26966 0.22542 0.65419
ya 0.18773 1.2677 0.031241 0.62269 -0.081441 0.68537 -0.36275 2.9738 -0.72967 1.035 0.41136 -0.99949 -2.8181 0.24364 0.51258 -0.51171 0.6693 -0.59732 -0.91591 0.23611 0.22535 0.42765 -0.7947 1.5532 0.1225
& -0.47122 0.056607 -0.29293 0.14845 -0.38806 0.98729 0.70408 1.1875 -0.11685 -0.022892 0.77426 0.54195 -4.7114 -0.50027 -0.44136 -0.29372 -0.31554 -0.58285 -0.1643 0.10002 -0.14504 -0.79716 -0.7261 0.2252 -0.17583
follow 0.0033407 0.91533 -1.2207 -0.45773 -0.59682 -0.64277 1.0497 1.7013 -1.3643 0.3601 -0.25219 -0.14811 -3.8711 -1.0949 -1.3944 0.22114 -0.76684 -2.0907 -1.0099 0.20968 -0.27403 -1.8368 -0.4521 0.8915 -1.0369
up -0.19555 0.8236 0.73457 0.12395 -0.21509 0.51058 1.1859 0.0058648 -0.18281 0.35138 -0.42667 0.66238 -5.3506 -0.066143 0.15166 -0.11217 0.25905 -1.2281 -0.63229 -0.49146 -0.2852 0.10816 1.0703 0.11823 -0.010115
what 0.5292 0.34413 -0.055991 0.15468 -0.48548 -0.42618 2.0155 -0.082657 -0.40249 0.066622 -0.56097 0.61953 -5.6142 -0.40026 0.54612 -0.021634 0.46933 -0.33373 0.096102 0.095193 0.53975 0.33677 -0.28179 0.50744 -0.51784
get -0.33344 1.2678 0.04472 -0.6707 -0.2079 0.12289 1.3696 -0.22981 -0.53645 -0.1833 -0.13394 0.63001 -5.6577 -0.66158 -0.26856 -0.1472 0.71835 -1.1591 -0.055771 -0.8732 -0.025146 0.3069 1.0787 0.38923 -0.028963
lol 0.073266 0.069397 0.15877 -0.20805 -0.43151 -0.26647 1.3905 0.48968 -0.73748 0.78262 -1.1841 0.1629 -4.6268 -0.76179 0.80136 0.78043 0.39787 -0.9309 -1.41 0.32624 1.2311 0.42486 0.70665 0.76985 0.20826
un -0.10621 0.057591 -0.752 1.3185 0.79391 0.56179 -0.85496 3.275 -0.45897 -0.35925 1.7636 -2.7374 -2.2786 0.11344 1.8262 0.91508 0.30052 0.35935 -2.1484 0.12763 0.17556 -0.79025 1.0724 -0.76144 0.37949
♥ -0.84469 -1.0147 -0.2948 0.50243 -0.032096 -0.25413 1.7008 2.7719 -2.0656 -0.016464 -0.10534 0.0078914 -1.8015 0.04799 -0.96726 -1.0318 -1.3104 -0.51772 -1.1396 0.53056 0.02979 -0.82598 0.19418 2.0574 0.50733
lo 0.67317 0.46962 -1.0861 0.70384 -0.033311 0.0016168 -0.20346 4.6008 0.083431 0.087919 1.3443 -2.0923 -1.781 0.069451 1.2344 1.1293 -0.13422 -0.1458 -0.15684 0.087938 0.31166 0.20576 -0.015365 1.2647 -0.26626
when -0.26148 0.2644 0.44876 0.1599 -0.47692 -0.31942 2.1561 -0.52634 -0.56854 0.28894 -0.3091 0.69452 -5.6008 -0.18411 0.075871 0.69657 0.35998 -0.64724 0.34793 -0.5933 0.57665 0.30556 0.48815 -0.11032 -0.78019
was -0.16063 0.021235 0.95695 -1.0642 -0.42496 0.070767 0.88473 -0.38835 -0.96585 -0.032367 0.2431 1.4682 -5.7357 -0.31611 0.59085 0.33569 0.92369 1.0457 -0.96856 -0.30444 0.65033 0.94053 -0.003684 0.14969 0.38408
“ 1.1393 0.31722 0.33893 0.59917 0.41805 0.26417 1.5744 2.0874 -0.38514 0.47434 0.3168 0.093502 -2.9127 -0.14853 -0.43053 -0.97776 -0.56379 0.31383 -0.67353 -0.63432 0.88654 -0.22208 -0.12107 -0.19183 0.6994
” 0.74133 -0.56073 0.0037826 0.25398 0.64676 -0.03136 1.5837 1.5481 -1.3584 0.62118 -0.14075 0.17492 -3.2719 -0.011897 -0.16072 -0.57518 -0.55753 0.22912 -0.49103 -0.25186 0.97739 -0.30327 0.39648 0.28217 1.0422
one 0.39657 0.15653 0.50676 -0.039995 -0.1177 -0.011625 1.7677 0.33504 -0.84748 -0.27969 0.036325 -0.146 -5.2788 0.053348 -0.60437 0.26285 0.15334 -0.31598 -0.18437 -0.21645 -0.095925 -0.07569 0.18185 -0.18519 -0.33499
por 0.98549 0.19405 0.77539 0.44123 0.58736 0.55549 -1.4343 2.9726 -1.1735 -1.2678 0.15086 -3.3556 -2.1731 -0.41532 1.1496 -0.46623 -1.331 0.71864 0.64299 -0.42066 0.51122 -0.81006 0.44971 0.087221 0.35618
si 0.31329 -0.29282 -0.88699 0.45418 -0.77082 -0.55735 -0.23928 4.1561 -0.27757 0.1545 0.9518 -2.3782 -1.9816 -0.11735 1.1881 1.358 0.56444 0.24605 -0.98873 0.64185 0.35727 -0.078937 -0.28172 0.88359 -0.51221
out -0.28653 0.60501 0.62592 -0.034889 -0.10508 0.063965 1.1527 -0.18502 -0.22128 0.29563 -0.061197 0.71973 -5.4451 -0.055855 0.078477 -0.0090364 0.32605 -0.90771 -0.53689 -0.34474 -0.3713 -0.17721 0.87016 -0.15274 0.026154

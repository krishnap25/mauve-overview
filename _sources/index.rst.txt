


MAUVE: Statistical Evaluation of LLMs and Generative AI
=========================================================================

.. raw:: html

    <div style="text-align: center">
        <table align=center>
            <tr> 
                <h5 style="font-weight:normal, text-align: center">
                    <a href="https://krishnap25.github.io">Krishna Pillutla</a><sup>1*</sup>,
                    <a href="https://langliu95.github.io/">Lang Liu</a><sup>2*</sup>,
                    <a href="https://johnthickstun.com/">John Thickstun</a><sup>3</sup>,
                    <a href="https://wellecks.com/">Sean Welleck</a><sup>4</sup>,
                    <a href="https://swabhs.com/"> Swabha Swayamdipta </a><sup>5</sup>, <br>
                    <a href="https://rowanzellers.com/">Rowan Zellers</a><sup>6</sup>,
                    <a href="https://homes.cs.washington.edu/~sewoong/">Sewoong Oh</a><sup>7</sup>,
                    <a href="https://homes.cs.washington.edu/~yejin/">Yejin Choi</a><sup>7, 8</sup>,
                    <a href="http://faculty.washington.edu/zaid/">Zaid Harchaoui</a><sup>7</sup>
                </h5>
            </tr>
            <tr>
                  <h6 style="font-weight:normal">
                    <sup>1</sup>IIT Madras,
                    <sup>2</sup>Citadel Securities,
                    <sup>3</sup>Stanford University,
                    <sup>4</sup>CMU, 
                    <sup>5</sup>USC,
                    <sup>6</sup>OpenAI, <br>
                    <sup>7</sup>University of Washington, 
                    <sup>8</sup>Allen Institute for Artificial Intelligence
                    <br>
                    <sup>*</sup>Equal Contribution
                  </h6>
            </tr>
            <tr>
                  <h4 style="font-weight:normal">
                    <i><b>NeurIPS 2021 Outstanding Paper Award</b></i>
                  </h4>
            </tr>
            <tr>
                  <h4 style="font-weight:normal">
                    <b>Papers</b>:
                    <a href="https://www.jmlr.org/papers/volume24/23-0023/23-0023.pdf">
                      JMLR '23</a>,  &nbsp; 
                    <a href="https://arxiv.org/pdf/2102.01454">
                      NeurIPS '21a</a>,  
                    <a href="https://arxiv.org/pdf/2106.07898">
                      NeurIPS '21b</a>  
                    <br> <br>
                    <b>Software</b>:
                    <a href="https://github.com/krishnap25/mauve">
                      Pip Package</a>,  &nbsp; 
                    <a href="https://huggingface.co/spaces/evaluate-metric/mauve">
                      HuggingFace Evaluate</a>,  &nbsp; 
                    <a href="https://github.com/krishnap25/mauve-experiments">
                      Full Code
                    </a>  &nbsp; 
                  </h4>
            </tr>
        </table>
    </div>

..
    This is a comment


.. image:: fig/illustration.png
    :width: 900px
    :align: center
    :alt: alternate text


Generative artificial intelligence has made significant strides, producing text indistinguishable from human prose and remarkably photorealistic images and videos. Automatically measuring how close the generated data distribution is to the target distribution is central to diagnosing existing models and developing better ones. We present MAUVE, a family of comparison measures between pairs of distributions such as those encountered in the generative modeling of text or images. These scores are statistical summaries of divergence frontiers capturing two types of errors in generative modeling. We explore three approaches to statistically estimate these scores: vector quantization, non-parametric estimation, and classifier-based estimation. We provide statistical bounds for the vector quantization approach.

Empirically, we find that the proposed scores paired with a range of 
*f*-divergences and statistical estimation methods can quantify the gaps between the distributions of human-written text and those of modern neural language models by correlating with human judgments and identifying known properties of the generated texts. We demonstrate in the vision domain that MAUVE can identify known properties of generated images on par with or better than existing metrics. In conclusion, we present practical recommendations for using MAUVE effectively with language and image modalities.

Empirical Results
------------------

.. raw:: html

    <div style="text-align: center">
        <table align=center>
            <tr> 
                <h3 style="font-weight:normal, text-align: center">
                    Measuring the Gap Between Model-Generated Text and Human Text
                </h3>
            </tr>
        </table>
    </div>

**MAUVE correlates better with human judgements** when compared to prior metrics. A A larger Spearman rank correlation means that the ranking of models obtained from the metric is closer to with the ranking derived from human judgements. We see that MAUVE's correlations are closer to 1, implying near perfect correlation.

.. image:: fig/results1.png
    :width: 900px
    :align: center
    :alt: alternate text

**MAUVE quantifies trends that were previously observed qualitatively**. For instance, larger models are generally better, longer generations are generally worse:

.. image:: fig/results2.png
    :width: 800px
    :align: center
    :alt: alternate text

.. raw:: html

    <div style="text-align: center">
        <table align=center>
            <tr> 
                <h3 style="font-weight:normal, text-align: center">
                    Measuring the Gap Between Generated and Real Images
                </h3>
            </tr>
        </table>
    </div>


**MAUVE identifies known properties of generated images** on par with or better than previous metrics, for instance, with the sampling algorithm (here, we vary the truncation parameter for StyleGAN2-ADA)...

.. image:: fig/results3.png
    :width: 800px
    :align: center
    :alt: alternate text

\.\.\. and with architectural improvements (here, we plot different versions of the StyleGAN model).

.. image:: fig/results4.png
    :width: 800px
    :align: center
    :alt: alternate text


Theoretical Results
--------------------

The estimation of MAUVE involves two errors: from quantization and from estimating the divergences from samples.

.. image:: fig/theory1.png
    :width: 500px
    :align: center
    :alt: alternate text

We bound both types of errors and consider smoothed distribution estimators that are **better both in theory and in practice**.

.. image:: fig/theory2.png
    :width: 900px
    :align: center
    :alt: alternate text

Other Detailed Results
-----------------------

We also have several detailed comparisons and ablation studies in the paper:

* **Experimental Domains**: Story and news article generations (language domain), and GAN vs. diffusion models (image domain)
* **Baselines**: comparison to generative precision-recall, and metrics based on optimal transport
* **Methodological Choices**: Comparison to other *f*-divergences; effect of varying the embedding: various types of LLMs and classical string kernel embedding
* **Algorithmic Choices**: Comparison of different estimation methods: non-parametric nearest neighbors and kernel density estimators, classifier-based estimation, and parametric approximation

These studies demonstrate the strong robustness of MAUVE and justify the various design choices involved.

Software Demo
--------------

Install the software with ``pip install mauve-text`` or use via HuggingFace Evaluate
as follows:

.. code-block:: python

    >>> import mauve   # pip install mauve-text
    >>> p_text = ...  # list of strings
    >>> q_text = ...  # list of strings
    >>> out = mauve.compute_mauve(p_text=p_text, q_text=q_text, device_id=0, verbose=False)
    >>> print(out.mauve) # prints a number between 0 and 1


.. raw:: html

    For more details, please see the documentation of 
    <a href="https://krishnap25.github.io/mauve/"><b>MAUVE pip package</b></a> or 
    <a href="https://huggingface.co/spaces/evaluate-metric/mauve"><b>MAUVE's page on HuggingFace Evaluate</b></a>.


References (`Bibtex <_static/bibtex.bib>`_)
-------------------------------------------

[1]  Pillutla, K., Liu, L., Thickstun, J., Welleck, S., Swayamdipta, S., Zellers, R., Oh, S., Choi, Y. and Harchaoui, Z., 2023. **MAUVE Scores for Generative Models: Theory and Practice**. *Journal of Machine Learning Research*, 24(356), pp.1-92.

[2] Pillutla, K., Swayamdipta, S., Zellers, R., Thickstun, J., Welleck, S., Choi, Y. and Harchaoui, Z., 2021. **MAUVE: Measuring the Gap Between Neural Text and Human Text using Divergence Frontiers**. *Proc. of NeurIPS* pp.4816-4828.

[3] Liu, L., Pillutla, K., Welleck, S., Oh, S., Choi, Y. and Harchaoui, Z., 2021. **Divergence Frontiers for Generative Models: Sample Complexity, Quantization Effects, and Frontier Integrals**. *Proc. of NeurIPS* pp.12930-12942.

Acknowledgments
----------------
Part of this work was done while Zaid Harchaoui was visiting the Simons Institute for
the Theory of Computing, and while Krishna Pillutla, Lang Liu, John Thickstun, Sean Welleck, and Rowan Zellers were at the University of Washington, and Swabha Swayamdipta was at the Allen Insitute for AI. This work was supported by NSF
DMS-2134012, NSF CCF-2019844, NSF DMS-2023166, the DARPA MCS program through
NIWC Pacific (N66001-19-2-4031), the CIFAR “Learning in Machines & Brains” program,
a Qualcomm Innovation Fellowship, and faculty research awards.
# Compressing a Model to FP16 {#openvino_docs_MO_DG_FP16_Compression}

@sphinxdirective

By default, when IR is saved all relevant floating-point weights are compressed to ``FP16`` data type during model conversion.
It results in creating a "compressed ``FP16`` model", which occupies about half of 
the original space in the file system. The compression may introduce a minor drop in accuracy,
but it is negligible for most models.
In case if accuracy drop is significant user can disable compression explicitly.

To disable compression, use the ``compress_to_fp16=False`` option:

.. tab-set::

    .. tab-item:: Python
       :sync: py

       .. code-block:: py
          :force:

          from openvino.runtime import save_model
          ov_model = save_model(INPUT_MODEL, compress_to_fp16=False)

    .. tab-item:: CLI
       :sync: cli

       .. code-block:: sh

          mo --input_model INPUT_MODEL --compress_to_fp16=False


For details on how plugins handle compressed ``FP16`` models, see 
:doc:`Working with devices <openvino_docs_OV_UG_Working_with_devices>`.

.. note::

   ``FP16`` compression is sometimes used as the initial step for ``INT8`` quantization. 
   Refer to the :doc:`Post-training optimization <pot_introduction>` guide for more 
   information about that.


.. note::

   Some large models (larger than a few GB) when compressed to ``FP16`` may consume an overly large amount of RAM on the loading
   phase of the inference. If that is the case for your model, try to convert it without compression: 
   ``convert_model(INPUT_MODEL, compress_to_fp16=False)`` or ``convert_model(INPUT_MODEL)``


@endsphinxdirective

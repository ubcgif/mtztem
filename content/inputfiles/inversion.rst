.. _mtztem_input_inv:

Inversion Input File
====================

The lines of input file for **ZTEM_MTinv.exe** are as follows:

.. tabularcolumns:: |L|C|C|

+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| Line # | Description                                                        | Description                                                       |
+========+====================================================================+===================================================================+
| 1      | :ref:`Tensor mesh<mtztem_input_inv_ln1>`                           | path to tensor mesh file                                          |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 2      | :ref:`Background conductivity<mtztem_input_inv_ln2>`               | set background conductivity for                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 3      | :ref:`Observation file<mtztem_input_inv_ln3>`                      | path to observations file                                         |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 4      | :ref:`Initial model<mtztem_input_inv_ln4>`                         | initial model                                                     |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 5      | :ref:`Reference model<mtztem_input_inv_ln5>`                       | reference model                                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 6      | :ref:`Background susceptibility <mtztem_input_inv_ln6>`            | background susceptibility model                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 7      | :ref:`Topography<mtztem_input_inv_ln7>`                            | topography/active cells                                           |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 8      | :ref:`Bounds<mtztem_input_inv_ln8>`                                | upper and lower bounds for cells                                  |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 9      | :ref:`Sensitivity weights<mtztem_input_inv_ln9>`                   | additional cell weights                                           |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 10     | :ref:`Trade-off parameter settings<mtztem_input_inv_ln10>`         | cooling schedule for beta parameter                               |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 11     | :ref:`alpha_s alpha_x alpha_y alpha_z<mtztem_input_inv_ln11>`      | weighting constants for smallness and smoothness constraints      |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 12     | :ref:`Reference model<mtztem_input_inv_ln12>`                      | stopping criteria for inversion                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 13     | :ref:`Hard constraints<mtztem_input_inv_ln13>`                     | set the number of Gauss-Newton iteration for each beta value      |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 14     | :ref:`Model type<mtztem_input_inv_ln14>`                           | set the tolerance and number of iterations for Gauss-Newton solve |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 15     | :ref:`Chi factor<mtztem_input_inv_ln15>`                           | reference model                                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 16     | :ref:`Methpar<mtztem_input_inv_ln16>`                              | use *SMOOTH_MOD* or *SMOOTH_MOD_DIFF*                             |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 17     | :ref:`tol_nl mindm iter_per_beta<mtztem_input_inv_ln17>`           | upper and lower bounds for recovered model                        |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 18     | :ref:`into max_linit<mtztem_input_inv_ln18>`                       | set solver parameters for iterative inversion                     |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 19     | :ref:`fortol initol<mtztem_input_inv_ln19>`                        | set solver parameters for iterative inversion                     |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 20     | :ref:`max_it_bicg droptol droptol_WTW<mtztem_input_inv_ln20>`      | set BICG tolerances                                               |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+



.. figure:: images/create_inv_input.png
     :align: center
     :width: 700

     Example input file for the inversion program (`Download <https://github.com/ubcgif/mtztem/raw/master/assets/input_files1/mtztem_octree_inv.inp>`__ ).


Line Descriptions
^^^^^^^^^^^^^^^^^

.. _mtztem_input_inv_ln1:

    - **Tensor Mesh:** file path to the OcTree mesh file

.. _mtztem_input_inv_ln2:

    - **Background Conductivity:** 

        - The user may supply the file path to a `1D background conductivity model <http://em1dfm.readthedocs.io/en/latest/content/files/supporting.html#files-for-reference-and-starting-models>`__ .
        - If a homogeneous background conductivity is being used, the user enters the value in S/m.

.. _mtztem_input_inv_ln3:

    - **Observation File:** file path to the :ref:`observed data file<obsFile>`

.. _mtztem_input_inv_ln4:

    - **Initial Model:** 

        - The user may supply the file path to an initial :ref:`conductivity model<modelFile>`.
        - If a homogeneous conductivity value is being used for all active cells, the user can enter the value in S/m.

.. _mtztem_input_inv_ln5:

    - **Reference Model:**

        - The user may supply the file path to a reference :ref:`conductivity model<modelFile>`.
        - If a homogeneous conductivity value is being used for all active cells, the user can enter the value in S/m.

.. _mtztem_input_inv_ln6:

    - **Background Susceptibility Model:**

        - The user may supply the file path to a background :ref:`susceptibility model<modelFile>`.
        - If a homogeneous susceptibility value is being used for all active cells, the user can enter the value in SI.
        - If the Earth is non-magnetic, the user may use the flag "NO_SUS".

.. _mtztem_input_inv_ln7:

    - **Topography:** Here, the user can choose to specify the cells which lie below the surface topography. Cells above the surface topography are given a value of :math:`\sigma = 10^{-8}` S/m and :math:`\chi=0` SI in the inversion. To set the topography, the user may:

        - use the flag *TOPO_FILE* followed by the file path to a :ref:`topography file<topoFile>`
        - use the flag *TOPO_CONST* followed by the value in meters if a constant elevation is being used
        - use the flag *MNZ* followed by the file path to an :ref:`active cells model file<modelActiveFile>`

.. _mtztem_input_inv_ln8:

    - **Bounds:** 

        - use the flag "BOUNDS_NONE" for no upper and lower bounds on recovered conductivities
        - use the flag "BOUNDS_CONST" followed by a value for the lower and upper bounds, respectively, to apply the same bounds to all cells (example: *BOUNDS_CONST 1E-10 0.1*)
        - use the flag "BOUNDS_FILE" followed by the file path to a :ref:`bounds file<boundsFile>` 

.. _mtztem_input_inv_ln9:

    - **Sensitivity Weights:** Here, the user specifies whether sensitivity weighting is applied. To set the sensitivity weighting:

        - use the flag *NONE* if no sensitivity weighting is being applied
        - or provide the filepath to a :ref:`weights file<weightsFile>`

.. _mtztem_input_inv_ln10:

    - **Trade-Off Parameter Settings:** Here, the user specifies the protocols for the `trade-off parameter <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Beta.html>`__ (:math:`\beta` ) between the data misfit and the model objective function. The protocols for the trade-off parameter are specified by three values: *beta_max* (starting :math:`\beta`), *beta_min* (lowest :math:`\beta` before inversion is terminated) and *beta_factor* (fractional decrease in :math:`\beta` each iteration - value between 0 and 1). There are two options for setting the trade-off parameter:

        - use the flag *DEFAULT*. In this case, where :math:`\mathbf{J}` is the sensitivity matrix, :math:`\mathbf{W}` is a linear regularization operator and :math:`\mathbf{r}` is a random vector:

                                .. math::
                                    \begin{align}
                                    beta \; start &= 1000 \times \frac{\| Jr \|^2}{\| Wr \|^2} \\
                                    beta \; end &= 10^{-7} \times beta \; start \\
                                    beta \; factor &= 0.16681
                                    \end{align}

        - or enter the values for *beta_start*, *beta_end* and *beta_factor* separated by spaces (example: *1E4 1E-2 0.2* )


.. _mtztem_input_inv_ln11:

    - **alpha_s alpha_x alpha_y alpha_z:** `Alpha parameters <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Alphas.html>`__ . Here, the user specifies the relative weighting between the smallness and smoothness component penalties on the recovered models. As a default setting, *alpha_x=alpha_y=alpha_z=1* and *alpha_s=1/h* :math:`\!^2` is suggested, where *h* is the average dimension of cells in the core region.

.. _mtztem_input_inv_ln12:

    - **Reference Model Update:** Here, the user specifies whether the reference model is updated at each inversion step result:

        - use the flag *CHANGE_MREF* if the reference model is updated at each iteration
        - use the flag *NOT_CHANGE_MREF* for the reference model to remain the same throughout the entire inversion

.. _mtztem_input_inv_ln13:

    - **Hard Constraints:** Here, the user specifies whether how the reference model is used to constrain the inversion; go to `fundamentals of inversion <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/MrefInSmooth.html>`__ to see how this is implemented. For the MTZTEM package:

        - use the flag *SMOOTH_MOD* to ignore the reference model (essential set :math:`m_{ref}=0` )
        - use the flag *SMOOTH_MOD_DIF* to include :math:`m_{ref}` in the smallness and smoothness penalty terms


.. _mtztem_input_inv_ln14:

    - **Model Type:** Here, the user specifies whether the model representing the Earth's conductivity is a log-conductivity or electrical resistivity model. Although the output model is a conductivity model, this choice will have an impact on how the sensitivity is computed:

        - use the flag *USE_LOG_COND* to define the model as a log-conductivity model
        - use the flag *USE_RES* to define as an electrical resistivity model


.. note:: It is suggested that *USE_LOG_COND* be used unless there is reason to do otherwise.


.. _mtztem_input_inv_ln15:

    - **Chi Factor:** The chi factor defines the target data misfit for the inversion. Once the target misfit is reached, the recovered model fits the field observations sufficiently without fitting the noise and the inversion ceases. A chi factor of 1 means the target misfit is equal to the total number of data observations. For more, see `fundamentals of inversion <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Beta.html#chi-factor>`__ .

.. _mtztem_input_inv_ln16:

    - **Methpar:** This line is used to specify parallelization options. Currently, only one option is available and this line should be set to a flag of *0* .

.. _mtztem_input_inv_ln17:

    - **tol_nl mindm iter_per_beta:** Here, the user specifies parameters related to the number of Newton iterations at each trade-off parameter (:math:`\beta` ) value. *tol_nl* is a tolerance on Newton iterations. The model is considered optimal when the gradient components of the current iteration are sufficiently smaller than those of the initial iteration multiplied by the tolerance. *mindm* is the minimum model perturbation. The Newton iterations stop when if the largest value in the current model is smaller than *mindm* . *iter_per_beta* maximum number of Newton iterations for a fixed trade-off parameter. To set these parameters:

        - use the flag *DEFAULT*, in which case *tol_nl* = 0.01, *mindm* = 0.001 and *iter_per_beta* = 5.
        - or set *tol_nl*, *mindm* and *iter_per_beta* in order separated by spaces

.. _mtztem_input_inv_ln18:

    - **intol max_linit:** Here, the user specifies solver parameters. *intol* specifies the tolerance for the linear solver (ipcg). This parameters find the optimal model perturbation size (typically between 0.001 and 0.1). *max_linit* sets the maximum number of iterations for the linear solver.

        - use the flag *DEFAULT*, in which case *intol* = 0.01 and *max_linit* = 10
        - or set *intol*, and *max_linit* in order separated by spaces

.. _mtztem_input_inv_ln19:

    - **fortol initol:** the parameter *fortol* sets the stop tolerance for forward and adjoint calculations when evaluating the objective function and gradients. This should be very small (:math:`\sim 10^{-9}` ). *initol* sets the stop tolerance for the forward and adjoint calculations inside the linear solver (ipcg). This tolerance can be larger than “fortol” to save time (typical 0.001 and lower).

        - use the *DEFAULT* flag, in which case *fortol* = :math:`10^{-9}` and *initol* = :math:`10^{-8}`
        - or set *fortol*, and *initol* in order separated by spaces

.. _mtztem_input_inv_ln20:

    - **max_it_bicg droptol droptol_WTW:** Here, *max_it_bicg* set the maximum number of iterations in BiCGSTAB when performing the forward and adjoint calculations. *droptol* sets the drop tolerance for the ILU preconditioner for the A matrix. And *droptol_WTW* sets the drop tolerance for the ILU preconditioner for the WTW matrix. This is used when the algorithm is looking for optimal model step size, and in the IPCG solver.

        - use the *DEFAULT* flag, in which case *max_it_bicg* = 15, *droptol* = 0.01 and *droptol_WTW* = 0.01
        - or set *max_it_bicg*, *droptol* and *droptol_WTW* in order separated by spaces
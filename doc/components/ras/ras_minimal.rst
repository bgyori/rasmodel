.. _ras_minimal:

Ras (minimal)
=============

This passage was processed and assembled automatically by INDRA:

  SOS1, bound to GRB2 binds RAS. RAS, bound to SOS1, binds GTP.


INDRA-assembled model components
--------------------------------

::

    from pysb import Monomer, Parameter, Rule, Annotation, ANY
    from pysb.util import alias_model_components

    def ras_minimal():
        Monomer('GTP', ['ras'])
        Monomer('RAS', [u'sos1', 'gtp', 'raf'])

        Parameter(u'kf_sr_bind_1', 1e-06)
        Parameter(u'kr_sr_bind_1', 1e-06)
        Parameter('kf_rg_bind_1', 1e-06)
        Parameter('kr_rg_bind_1', 1e-06)

        alias_model_components()

        Rule(u'SOS1_GRB2_RAS_bind', SOS1(grb2=ANY, ras=None) + RAS(sos1=None) >>
            SOS1(grb2=ANY, ras=1) % RAS(sos1=1), kf_sr_bind_1)

        Rule(u'SOS1_GRB2_RAS_dissociate', SOS1(ras=1) % RAS(sos1=1) >>
            SOS1(ras=None) + RAS(sos1=None), kr_sr_bind_1)

        Rule(u'RAS_SOS1_GTP_bind', RAS(sos1=ANY, gtp=None) + GTP(ras=None) >>
            RAS(sos1=ANY, gtp=1) % GTP(ras=1), kf_rg_bind_1)

        Rule(u'RAS_SOS1_GTP_dissociate', RAS(gtp=1) % GTP(ras=1) >>
            RAS(gtp=None) + GTP(ras=None), kr_rg_bind_1)

        Annotation(GTP, 'http://identifiers.org/chebi/CHEBI:37565', 'is')
        Annotation(RAS, 'http://identifiers.org/pfam/PF00071.18', 'is')
        Annotation(RAS, 'http://identifiers.org/chebi/CHEBI:63620', 'is')

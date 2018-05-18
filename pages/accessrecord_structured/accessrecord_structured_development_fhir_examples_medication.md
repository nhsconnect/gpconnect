---
title: FHIR&reg; Medication examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_medication.html
summary: "Access Record Structured FHIR examples"
---



The following is a set of request/response examples for Medication:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
<!--    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Example 2</a></li>
    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>
  <div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Example 1</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient's structured record:</p>

<ul>
  <li>Medication</li>
  <li>Prescription Issues</li>
</ul>


<p style="line-height: 1; font-size: 18px">Request payload</p>

<p>Note: The <code class="highlighter-rouge">includePrescriptionIssues</code> parameter has explicitly been set to <code class="highlighter-rouge">true</code>.</p>

<div class="language-json highlighter-rouge">
<pre class="highlight"><code><span class="p">{</span><span class="w">
  </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Parameters"</span><span class="p">,</span><span class="w">
  </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
    </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
      </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1"</span><span class="w">
    </span><span class="p">}</span><span class="w">
  </span><span class="p">},</span><span class="w">
  </span><span class="nt">"parameter"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
    </span><span class="p">{</span><span class="w">
      </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"patientNHSNumber"</span><span class="p">,</span><span class="w">
      </span><span class="nt">"valueIdentifier"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
        </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/Id/nhs-number"</span><span class="p">,</span><span class="w">
        </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"9999999999"</span><span class="w">
      </span><span class="p">}</span><span class="w">
    </span><span class="p">},</span><span class="w">
    </span><span class="p">{</span><span class="w">
      </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includeMedication"</span><span class="p">,</span><span class="w">
      </span><span class="nt">"part"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
        </span><span class="p">{</span><span class="w">
          </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includePrescriptionIssues"</span><span class="p">,</span><span class="w">
          </span><span class="nt">"valueBoolean"</span><span class="p">:</span><span class="w"> </span><span class="kc">true</span><span class="w">
        </span><span class="p">}</span><span class="w">
      </span><span class="p">]</span><span class="w">
    </span><span class="p">}</span><span class="w">
  </span><span class="p">]</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre>
</div>

<p style="line-height: 1; font-size: 18px">Response payload</p>

<div class="language-json highlighter-rouge">
<pre class="highlight"><code><span class="p">{</span><span class="w">
   </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Bundle"</span><span class="p">,</span><span class="w">
   </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"79183513-1382-4cdd-9470-7dbad15ea7b0"</span><span class="p">,</span><span class="w">
   </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"collection"</span><span class="p">,</span><span class="w">
   </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
      </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
         </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1"</span><span class="w">
      </span><span class="p">],</span><span class="w">
      </span><span class="nt">"lastUpdated"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="w">
   </span><span class="p">},</span><span class="w">
   </span><span class="nt">"entry"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"List"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"current"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"mode"</span><span class="p">:</span><span class="w"> </span><span class="s2">"snapshot"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"title"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication List"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"933361000000108"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medications and medical devices (record artifact)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
				</span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
					</span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
				</span><span class="p">},</span><span class="w">
            </span><span class="nt">"date"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"orderedBy"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"event-date"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://hl7.org/fhir/list-order"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"entry"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationStatement/6bff710a-0bdc-4c9b-b98b-40db0a107edc"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationStatement/791ceb40-db0a-491d-ab0f-22f5a08509fd"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
		</span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationStatement"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"6bff710a-0bdc-4c9b-b98b-40db0a107edc"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationStatementLastIssueDate-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueDateTime"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"basedOn"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest/7e68abae-a50a-4dd2-8445-7a2aa9936bee"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"completed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/c260b451-9821-42de-81f9-ba86dcea2c32"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"effectiveDateTime"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"dateAsserted"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"taken"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unk"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Pharmacy Notes: NOTES FOR PHARMACY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosage"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE DAILY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">         
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
		 </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"c260b451-9821-42de-81f9-ba86dcea2c32"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"56966201000001112"</span><span class="w">
                              </span><span class="p">},</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Amoxicillin 250mg capsules"</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">],</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Product containing amoxicillin 250 mg/1 each oral capsule (clinical drug)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"323509004"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">}</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"7e68abae-a50a-4dd2-8445-7a2aa9936bee"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"completed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"intent"</span><span class="p">:</span><span class="w"> </span><span class="s2">"plan"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/c260b451-9821-42de-81f9-ba86dcea2c32"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"authoredOn"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Pharmacy Notes: NOTES FOR PHARMACY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosageInstruction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE DAILY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dispenseRequest"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"expectedSupplyDuration"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"d"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"unit"</span><span class="p">:</span><span class="w"> </span><span class="s2">"day"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://unitsofmeasure.org"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"quantity"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"capsule(s)"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"validityPeriod"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"start"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueCodeableConcept"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"acute"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Acute"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"ca89c863-1569-4e0f-ae8c-31bf98367555"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"basedOn"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest/7e68abae-a50a-4dd2-8445-7a2aa9936bee"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"completed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"intent"</span><span class="p">:</span><span class="w"> </span><span class="s2">"order"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/c260b451-9821-42de-81f9-ba86dcea2c32"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"authoredOn"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"NOTES FOR PHARMACY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosageInstruction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE DAILY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dispenseRequest"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"expectedSupplyDuration"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"d"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"unit"</span><span class="p">:</span><span class="w"> </span><span class="s2">"day"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://unitsofmeasure.org"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"quantity"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"capsule(s)"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"validityPeriod"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"start"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-05-10"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueCodeableConcept"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"acute"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Acute"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationStatement"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"791ceb40-db0a-491d-ab0f-22f5a08509fd"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-CareConnect-MedicationStatementLastIssueDate-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueDateTime"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-09-11"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"basedOn"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest/8e078d04-8312-433a-b6b4-46bf52542b0c"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"active"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/8b339981-e9be-4e37-bf03-799295a6aec8"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"effectivePeriod"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"start"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-08-11"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"dateAsserted"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-08-11"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"taken"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unk"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"SOME NOTES"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosage"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE DAILY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"8b339981-e9be-4e37-bf03-799295a6aec8"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"56962301000001119"</span><span class="w">
                              </span><span class="p">},</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Aspirin 75mg dispersible tablets"</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">],</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Aspirin 75mg dispersible tablet (product)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"319773006"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">}</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"8e078d04-8312-433a-b6b4-46bf52542b0c"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"groupIdentifier"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"urn:uuid:eba24af1-5b74-4790-aa5a-2134fd27ad75"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"active"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"intent"</span><span class="p">:</span><span class="w"> </span><span class="s2">"plan"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/8b339981-e9be-4e37-bf03-799295a6aec8"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"authoredOn"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-08-11"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"NOTES FOR PHARMACY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosageInstruction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE 3 TIMES/DAY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dispenseRequest"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"expectedSupplyDuration"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"d"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"unit"</span><span class="p">:</span><span class="w"> </span><span class="s2">"day"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://unitsofmeasure.org"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"quantity"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"tablets(s)"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"84"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"validityPeriod"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"start"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-08-11"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationRepeatInformation-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"numberOfRepeatPrescriptionsAllowed"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valuePositiveInt"</span><span class="p">:</span><span class="w"> </span><span class="mi">5</span><span class="w">
                     </span><span class="p">},</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"numberOfRepeatPrescriptionsIssued"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valuePositiveInt"</span><span class="p">:</span><span class="w"> </span><span class="mi">2</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueCodeableConcept"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"repeat"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Repeat"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"8afe3af9-995d-4ccc-9211-f8c2620be670"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"basedOn"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest/8e078d04-8312-433a-b6b4-46bf52542b0c"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"groupIdentifier"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"urn:uuid:eba24af1-5b74-4790-aa5a-2134fd27ad75"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"completed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"intent"</span><span class="p">:</span><span class="w"> </span><span class="s2">"order"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/8b339981-e9be-4e37-bf03-799295a6aec8"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"authoredOn"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-08-11"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"NOTES FOR PHARMACY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosageInstruction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE 3 TIMES/DAY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dispenseRequest"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"expectedSupplyDuration"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"d"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"unit"</span><span class="p">:</span><span class="w"> </span><span class="s2">"day"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://unitsofmeasure.org"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"quantity"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"tablet(s)"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"84"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"validityPeriod"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"start"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-08-11"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueCodeableConcept"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"repeat"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Repeat"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"a946012a-283b-46c4-8312-e1312a54ab9c"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"basedOn"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"MedicationRequest/8e078d04-8312-433a-b6b4-46bf52542b0c"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"groupIdentifier"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"urn:uuid:eba24af1-5b74-4790-aa5a-2134fd27ad75"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"completed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"intent"</span><span class="p">:</span><span class="w"> </span><span class="s2">"order"</span><span class="p">,</span><span class="w">
	    </span><span class="nt">"medicationReference"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Medication/8b339981-e9be-4e37-bf03-799295a6aec8"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"authoredOn"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-09-11"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"NOTES FOR PHARMACY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dosageInstruction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"patientInstruction"</span><span class="p">:</span><span class="w"> </span><span class="s2">"INSTRUCTIONS FOR PATIENT"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TAKE ONE 3 TIMES/DAY"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"dispenseRequest"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"expectedSupplyDuration"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"d"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"28"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"unit"</span><span class="p">:</span><span class="w"> </span><span class="s2">"day"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://unitsofmeasure.org"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"quantity"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"tablet(s)"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"84"</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="nt">"validityPeriod"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"start"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-09-11"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"valueCodeableConcept"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"repeat"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Repeat"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
 		</span><span class="p">{</span><span class="w">
			</span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
				</span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient"</span><span class="p">,</span><span class="w">
				</span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="p">,</span><span class="w">
				</span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
					</span><span class="nt">"lastUpdated"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-09T07:52:45.466+00:00"</span><span class="p">,</span><span class="w">
					</span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
						</span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"</span><span class="w">
					</span><span class="p">]</span><span class="w">
				</span><span class="p">},</span><span class="w">
				</span><span class="nt">"identifier"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/Id/nhs-number"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"valueCodeableConcept"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"K3XZhBz91kCLWKuTUnEArg=='"</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"99999999"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
				</span><span class="nt">"active"</span><span class="p">:</span><span class="w"> </span><span class="kc">true</span><span class="p">,</span><span class="w">
				</span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="p">[{</span><span class="w">
					</span><span class="nt">"use"</span><span class="p">:</span><span class="w"> </span><span class="s2">"official"</span><span class="p">,</span><span class="w">
					</span><span class="nt">"family"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Munoz"</span><span class="p">,</span><span class="w">
					</span><span class="nt">"given"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
						</span><span class="s2">"Vicky"</span><span class="w">
					</span><span class="p">],</span><span class="w">
					</span><span class="nt">"prefix"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
						</span><span class="s2">"Mrs"</span><span class="w">
					</span><span class="p">]</span><span class="w">
				</span><span class="p">}],</span><span class="w">
				</span><span class="nt">"gender"</span><span class="p">:</span><span class="w"> </span><span class="s2">"female"</span><span class="p">,</span><span class="w">
				</span><span class="nt">"birthDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"1935-09-20"</span><span class="p">,</span><span class="w">
				</span><span class="nt">"generalPractitioner"</span><span class="p">:</span><span class="w"> </span><span class="p">[{</span><span class="w">
					</span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
				</span><span class="p">}]</span><span class="w">
			</span><span class="p">}</span><span class="w">
		</span><span class="p">},</span><span class="w">

		</span><span class="p">{</span><span class="w">
			</span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
				</span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
					</span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
						</span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-PractitionerRole-1"</span><span class="w">
					</span><span class="p">]</span><span class="w">
				</span><span class="p">},</span><span class="w">
				</span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole"</span><span class="p">,</span><span class="w">
				</span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="p">,</span><span class="w">
				</span><span class="nt">"practitioner"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
					</span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Practitioner/6c41ebfd-57c3-4162-9d7b-208c171a2fd7"</span><span class="w">
				</span><span class="p">},</span><span class="w">
				</span><span class="nt">"organization"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
					</span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Organization/db67f447-b30d-442a-8e31-6918d1367eeb"</span><span class="p">,</span><span class="w">
					</span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"The Moir Medical Centre"</span><span class="w">
				</span><span class="p">},</span><span class="w">
				</span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[{</span><span class="w">
					</span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[{</span><span class="w">
						</span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"</span><span class="p">,</span><span class="w">
						</span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"R0260"</span><span class="p">,</span><span class="w">
						</span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"General Medical Practitioner"</span><span class="w">
					</span><span class="p">}]</span><span class="w">
				</span><span class="p">}]</span><span class="w">
			</span><span class="p">}</span><span class="w">
		</span><span class="p">},</span><span class="w">


      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Practitioner"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"identifier"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/Id/sds-user-id"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"G8133438"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"family"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Bhatia"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"prefix"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Dr"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"given"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"John"</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"active"</span><span class="p">:</span><span class="w"> </span><span class="kc">true</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"6c41ebfd-57c3-4162-9d7b-208c171a2fd7"</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Organization"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"db67f447-b30d-442a-8e31-6918d1367eeb"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"identifier"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/Id/ods-organization-code"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"C81010"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"active"</span><span class="p">:</span><span class="w"> </span><span class="kc">true</span><span class="p">,</span><span class="w">
            </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"394745000"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"General practice (organisation) (qualifier value)"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"The Moir Medical Centre"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"telecom"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"phone"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"0115 9737320"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"use"</span><span class="p">:</span><span class="w"> </span><span class="s2">"work"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"address"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"use"</span><span class="p">:</span><span class="w"> </span><span class="s2">"work"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"both"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"line"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"The Moir Medical Centre"</span><span class="p">,</span><span class="w">
                     </span><span class="s2">"Regent Street, Long Eaton"</span><span class="p">,</span><span class="w">
                     </span><span class="s2">"Nottingham"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"city"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Nottingham"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"district"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Derbyshire"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"postalCode"</span><span class="p">:</span><span class="w"> </span><span class="s2">"NG10 1QQ"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">}</span><span class="w">
   </span><span class="p">]</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre>
</div>


</div>
<div role="tabpanel" class="tab-pane" id="example2">
<p style="line-height: 2; font-size: 20px">Example 2</p>
<p style="line-height: 1; font-size: 18px">Request</p>
<p>Example of a call to return the following items from a patient’s structured record:</p>
<ul>
  <li>Medication</li>
</ul>
<p style="line-height: 1; font-size: 18px">Request payload</p>
<p style="line-height: 1; font-size: 18px">Response payload</p>



</div>
<div role="tabpanel" class="tab-pane" id="example3">
<p style="line-height: 2; font-size: 20px">Example 3</p>
<p style="line-height: 1; font-size: 18px">Request</p>
<p>Example of a call to return the following items from a patient’s structured record:</p>
<ul>
  <li>Medication</li>
</ul>
<p style="line-height: 1; font-size: 18px">Request payload</p>
<p style="line-height: 1; font-size: 18px">Response payload</p>


</div>
</div>

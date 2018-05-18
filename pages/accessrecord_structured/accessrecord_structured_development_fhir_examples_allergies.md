---
title: FHIR&reg; Allergies examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_allergies.html
summary: "Access Record Structured FHIR examples"
---



The following is a set of request/response examples for Allergies:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Example 2</a></li>
    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li>
</ul>
  <div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Example 1</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient's structured record:</p>

<ul>
  <li>Allergies</li>
  <li>Resolved allergies</li>
</ul>


<p style="line-height: 1; font-size: 18px">Request payload</p>

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
      </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includeAllergies"</span><span class="p">,</span><span class="w">
      </span><span class="nt">"part"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
        </span><span class="p">{</span><span class="w">
          </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includeResolvedAllergies"</span><span class="p">,</span><span class="w">
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
   </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
      </span><span class="nt">"lastUpdated"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="p">,</span><span class="w">
      </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
         </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1"</span><span class="w">
      </span><span class="p">]</span><span class="w">
   </span><span class="p">},</span><span class="w">
   </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"collection"</span><span class="p">,</span><span class="w">
   </span><span class="nt">"entry"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"current"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"title"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Active Allergies"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Allergies and adverse reaction (record artifact)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"886921000000105"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"List"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"entry"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance/561850bd-360c-4d17-b3c8-a837ef0cbfba"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance/6bff710a-0bdc-4c9b-b98b-40db0a107edc"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance/5eb0f76a-cecb-4b83-999d-ddb76e551a9b"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">},</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance/d92b7d42-554d-4c92-b829-e76508185702"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"date"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"mode"</span><span class="p">:</span><span class="w"> </span><span class="s2">"snapshot"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"orderedBy"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://hl7.org/fhir/list-order"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"event-date"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">}</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"contained"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Resolved-1"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-AllergyIntoleranceEnd-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                           </span><span class="p">{</span><span class="w">
                              </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"endDate"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"valueDateTime"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-20-01T09:00:34+00:00"</span><span class="w">
                           </span><span class="p">},</span><span class="w">
                           </span><span class="p">{</span><span class="w">
                              </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"reasonEnded"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient reports no subsequent recurrence on same medication"</span><span class="w">
                           </span><span class="p">}</span><span class="w">
                        </span><span class="p">]</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"reaction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"manifestation"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                           </span><span class="p">{</span><span class="w">
                              </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                 </span><span class="p">{</span><span class="w">
                                    </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Vomiting (disorder)"</span><span class="p">,</span><span class="w">
                                    </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"422400008"</span><span class="p">,</span><span class="w">
                                    </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                                    </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                       </span><span class="p">{</span><span class="w">
                                          </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                                          </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                             </span><span class="p">{</span><span class="w">
                                                </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                                </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2647992016"</span><span class="w">
                                             </span><span class="p">},</span><span class="w">
                                             </span><span class="p">{</span><span class="w">
                                                </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                                </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Emesis"</span><span class="w">
                                             </span><span class="p">}</span><span class="w">
                                          </span><span class="p">]</span><span class="w">
                                       </span><span class="p">}</span><span class="w">
                                    </span><span class="p">]</span><span class="w">
                                 </span><span class="p">}</span><span class="w">
                              </span><span class="p">]</span><span class="w">
                           </span><span class="p">}</span><span class="w">
                        </span><span class="p">],</span><span class="w">
                        </span><span class="nt">"severity"</span><span class="p">:</span><span class="w"> </span><span class="s2">"severe"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"verificationStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unconfirmed"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"assertedDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2011-05-07"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"intolerance"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Aspirin 75mg dispersible tablet (product)"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"319773006"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
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
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">},</span><span class="w">
                  </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"clinicalStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"resolved"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"patient"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
                  </span><span class="p">},</span><span class="w">
                  </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Allergy Type: Adverse Reaction, Certainty: Absolute, Severity: Very Severe, NOTES: Some freetext notes"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
                  </span><span class="p">},</span><span class="w">
                  </span><span class="nt">"category"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"medication"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">},</span><span class="w">
                  </span><span class="nt">"criticality"</span><span class="p">:</span><span class="w"> </span><span class="s2">"low"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"current"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"title"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Resolved Allergies"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Resolved Allergies"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TBD"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"List"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"entry"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"#Resolved-1"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"date"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"mode"</span><span class="p">:</span><span class="w"> </span><span class="s2">"snapshot"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"orderedBy"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://hl7.org/fhir/list-order"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"event-date"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"identifier"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.nhs.uk/Id/nhs-number"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"1234567890"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">}</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"6bff710a-0bdc-4c9b-b98b-40db0a107edc"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"reaction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"manifestation"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                           </span><span class="p">{</span><span class="w">
                              </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"On examination - itchy rash (disorder)"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"304386008"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                 </span><span class="p">{</span><span class="w">
                                    </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                                    </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                       </span><span class="p">{</span><span class="w">
                                          </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                          </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"446685017"</span><span class="w">
                                       </span><span class="p">},</span><span class="w">
                                       </span><span class="p">{</span><span class="w">
                                          </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                          </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"O/E - itchy rash"</span><span class="w">
                                       </span><span class="p">}</span><span class="w">
                                    </span><span class="p">]</span><span class="w">
                                 </span><span class="p">}</span><span class="w">
                              </span><span class="p">]</span><span class="w">
                           </span><span class="p">}</span><span class="w">
                        </span><span class="p">]</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"severity"</span><span class="p">:</span><span class="w"> </span><span class="s2">"mild"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"verificationStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unconfirmed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"assertedDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2012-05-07T00:00+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"allergy"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Product containing amoxicillin 250 mg/1 each oral capsule (clinical drug)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"323509004"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
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
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"clinicalStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"active"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"patient"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Certainty: Likely, Severity: Minimal, NOTES: Some freetext notes"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"category"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="s2">"medication"</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"criticality"</span><span class="p">:</span><span class="w"> </span><span class="s2">"low"</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"5eb0f76a-cecb-4b83-999d-ddb76e551a9b"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"reaction"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"manifestation"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                           </span><span class="p">{</span><span class="w">
                              </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Peanut-induced anaphylaxis (disorder)"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"241933001"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                              </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                 </span><span class="p">{</span><span class="w">
                                    </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                                    </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                                       </span><span class="p">{</span><span class="w">
                                          </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                          </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"362151013"</span><span class="w">
                                       </span><span class="p">},</span><span class="w">
                                       </span><span class="p">{</span><span class="w">
                                          </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                          </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Peanut-induced anaphylaxis"</span><span class="w">
                                       </span><span class="p">}</span><span class="w">
                                    </span><span class="p">]</span><span class="w">
                                 </span><span class="p">}</span><span class="w">
                              </span><span class="p">]</span><span class="w">
                           </span><span class="p">}</span><span class="w">
                        </span><span class="p">]</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"severity"</span><span class="p">:</span><span class="w"> </span><span class="s2">"severe"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"verificationStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unconfirmed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"assertedDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-02-08T10:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"allergy"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Peanut - dietary (substance)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"256349002"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"381850016"</span><span class="w">
                              </span><span class="p">},</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Peanut - dietary"</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"clinicalStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"active"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"patient"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Certainty: Certain, Severity: Life Threatening, NOTES: notes on the peanut allergy"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"category"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="s2">"environment"</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"criticality"</span><span class="p">:</span><span class="w"> </span><span class="s2">"high"</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"d92b7d42-554d-4c92-b829-e76508185702"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"verificationStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unconfirmed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"allergy"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Transfer-degraded drug allergy (record artifact)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"196461000000101"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"294801000000114"</span><span class="w">
                              </span><span class="p">},</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Transfer-degraded drug allergy"</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"clinicalStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"active"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"patient"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"NOTES: This was entered incorrectly on the source system as a history/journal entry and not as a drug allergy"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"assertedDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2016-01-08T11:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"category"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="s2">"medication"</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">}</span><span class="w">
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
                                 </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"K3XZhBz91kCLWKuTUnEArg=="</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"value"</span><span class="p">:</span><span class="w"> </span><span class="s2">"99999999"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"active"</span><span class="p">:</span><span class="w"> </span><span class="kc">true</span><span class="p">,</span><span class="w">
            </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"use"</span><span class="p">:</span><span class="w"> </span><span class="s2">"official"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"family"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Munoz"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"given"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Vicky"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"prefix"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Mrs"</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"gender"</span><span class="p">:</span><span class="w"> </span><span class="s2">"female"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"birthDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"1935-09-20"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"generalPractitioner"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
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
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"R0260"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"General Medical Practitioner"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
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
  <li>Allergies</li>
</ul>

<p style="line-height: 1; font-size: 18px">Request payload</p>

<p>Note: The <code class="highlighter-rouge">includeResolvedAllergies</code> parameter has not been set - by default resolved allergies are NOT returned.</p>

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
      </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includeAllergies"</span><span class="w">
    </span><span class="p">}</span><span class="w">
  </span><span class="p">]</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre>
</div>

<p style="line-height: 1; font-size: 18px">Response payload</p>

<p>Assumption - ‘No Known Allergies’ has not been positively asserted on record, but is not contradicted by presence of active allergies on record.</p>

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
            </span><span class="nt">"title"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Active Allergies"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"date"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"List"</span><span class="p">,</span><span class="w">	
			</span><span class="nt">"mode"</span><span class="p">:</span><span class="w"> </span><span class="s2">"snapshot"</span><span class="p">,</span><span class="w">	
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"current"</span><span class="p">,</span><span class="w">			
			</span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Allergies and adverse reaction (record artifact)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"886921000000105"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"entry"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"item"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance/561850bd-360c-4d17-b3c8-a837ef0cbfba"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"orderedBy"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://hl7.org/fhir/list-order"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"event-date"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">}</span><span class="w">
         </span><span class="p">}</span><span class="w">
      </span><span class="p">},</span><span class="w">
      </span><span class="p">{</span><span class="w">
         </span><span class="nt">"resource"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
            </span><span class="nt">"id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"561850bd-360c-4d17-b3c8-a837ef0cbfba"</span><span class="p">,</span><span class="w">
			</span><span class="nt">"assertedDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2012-05-07T00:00+00:00"</span><span class="p">,</span><span class="w">
			</span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"AllergyIntolerance"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"clinicalStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"active"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"verificationStatus"</span><span class="p">:</span><span class="w"> </span><span class="s2">"unconfirmed"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"allergy"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"No known allergy (situation)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"716186003"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                        </span><span class="p">{</span><span class="w">
                           </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid"</span><span class="p">,</span><span class="w">
                           </span><span class="nt">"extension"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionID"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueId"</span><span class="p">:</span><span class="w"> </span><span class="s2">"3304950010"</span><span class="w">
                              </span><span class="p">},</span><span class="w">
                              </span><span class="p">{</span><span class="w">
                                 </span><span class="nt">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"DescriptionDisplay"</span><span class="p">,</span><span class="w">
                                 </span><span class="nt">"valueString"</span><span class="p">:</span><span class="w"> </span><span class="s2">"No known"</span><span class="w">
                              </span><span class="p">}</span><span class="w">
                           </span><span class="p">]</span><span class="w">
                        </span><span class="p">}</span><span class="w">
                     </span><span class="p">]</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"patient"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"recorder"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"category"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="s2">"medication"</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">}</span><span class="w">
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
            </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"use"</span><span class="p">:</span><span class="w"> </span><span class="s2">"official"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"family"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Munoz"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"given"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Vicky"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"prefix"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Mrs"</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"gender"</span><span class="p">:</span><span class="w"> </span><span class="s2">"female"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"birthDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"1935-09-20"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"generalPractitioner"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
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
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"R0260"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"General Medical Practitioner"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
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

<div role="tabpanel" class="tab-pane" id="example3">

<p style="line-height: 2; font-size: 20px">Example 3</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Allergies</li>
</ul>

<p style="line-height: 1; font-size: 18px">Request payload</p>

<p>Note: The <code class="highlighter-rouge">includeResolvedAllergies</code> parameter has explicitly been set to <code class="highlighter-rouge">false</code>.</p>

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
      </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includeAllergies"</span><span class="p">,</span><span class="w">
      </span><span class="nt">"part"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
        </span><span class="p">{</span><span class="w">
          </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"includeResolvedAllergies"</span><span class="p">,</span><span class="w">
          </span><span class="nt">"valueBoolean"</span><span class="p">:</span><span class="w"> </span><span class="kc">false</span><span class="w">
        </span><span class="p">}</span><span class="w">
      </span><span class="p">]</span><span class="w">
    </span><span class="p">}</span><span class="w">
  </span><span class="p">]</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre>
</div>

<p style="line-height: 1; font-size: 18px">Response payload</p>

<p>Assumes - ‘No Known Allergies’ has been positively asserted on record and is not contradicted by presence of active allergies on record.</p>

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
            </span><span class="nt">"meta"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"profile"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="s2">"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1"</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"status"</span><span class="p">:</span><span class="w"> </span><span class="s2">"current"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"title"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Active Allergies"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Allergies and adverse reaction (record artifact)"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://snomed.info/sct"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"886921000000105"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"resourceType"</span><span class="p">:</span><span class="w"> </span><span class="s2">"List"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"emptyReason"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://hl7.org/fhir/special-values"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"nocontentrecorded"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"No content recorded"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"note"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"text"</span><span class="p">:</span><span class="w"> </span><span class="s2">"There are no allergies in the patient record but it has not been confirmed with the patient that they have no allergies (that is, a ‘no known allergies’ code has not been recorded)."</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"date"</span><span class="p">:</span><span class="w"> </span><span class="s2">"2018-03-01T10:57:34+00:00"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"mode"</span><span class="p">:</span><span class="w"> </span><span class="s2">"snapshot"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"orderedBy"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                  </span><span class="p">{</span><span class="w">
                     </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://hl7.org/fhir/list-order"</span><span class="p">,</span><span class="w">
                     </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"event-date"</span><span class="w">
                  </span><span class="p">}</span><span class="w">
               </span><span class="p">]</span><span class="w">
            </span><span class="p">},</span><span class="w">
            </span><span class="nt">"subject"</span><span class="p">:</span><span class="w"> </span><span class="p">{</span><span class="w">
               </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"</span><span class="w">
            </span><span class="p">}</span><span class="w">
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
            </span><span class="nt">"name"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"use"</span><span class="p">:</span><span class="w"> </span><span class="s2">"official"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"family"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Munoz"</span><span class="p">,</span><span class="w">
                  </span><span class="nt">"given"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Vicky"</span><span class="w">
                  </span><span class="p">],</span><span class="w">
                  </span><span class="nt">"prefix"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="s2">"Mrs"</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">],</span><span class="w">
            </span><span class="nt">"gender"</span><span class="p">:</span><span class="w"> </span><span class="s2">"female"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"birthDate"</span><span class="p">:</span><span class="w"> </span><span class="s2">"1935-09-20"</span><span class="p">,</span><span class="w">
            </span><span class="nt">"generalPractitioner"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"reference"</span><span class="p">:</span><span class="w"> </span><span class="s2">"PractitionerRole/e0244de8-07ef-4274-9f7a-d7067bcc8d21"</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
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
            </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
               </span><span class="p">{</span><span class="w">
                  </span><span class="nt">"coding"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
                     </span><span class="p">{</span><span class="w">
                        </span><span class="nt">"system"</span><span class="p">:</span><span class="w"> </span><span class="s2">"https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"code"</span><span class="p">:</span><span class="w"> </span><span class="s2">"R0260"</span><span class="p">,</span><span class="w">
                        </span><span class="nt">"display"</span><span class="p">:</span><span class="w"> </span><span class="s2">"General Medical Practitioner"</span><span class="w">
                     </span><span class="p">}</span><span class="w">
                  </span><span class="p">]</span><span class="w">
               </span><span class="p">}</span><span class="w">
            </span><span class="p">]</span><span class="w">
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
</div>

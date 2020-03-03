libiec61850/
├── inc
└── src
    ├── common
    ├── goose
    ├── sampled_values
    ├── hal
    │   ├── ethernet
    │   ├── filesystem
    │   ├── socket
    │   └── thread
    ├── iedclient
    │   └── impl
    ├── iedcommon
    ├── iedserver
    │   ├── impl
    │   ├── mms_mapping
    │   └── model
    ├── mms
    │   ├── asn1
    │   ├── iso_acse
    │   ├── iso_client
    │   ├── iso_cotp
    │   ├── iso_mms
    │   │   ├── asn1c
    │   │   ├── client
    │   │   ├── common
    │   │   └── server
    │   ├── iso_presentation
    │   ├── iso_server
    │   └── iso_session
    └── vs


libiec61850/
├── inc
│   └── stack_config.h
├── src
│   ├── common
│   │   ├── array_list.c
│   │   ├── array_list.h
│   │   ├── buffer_chain.c
│   │   ├── buffer_chain.h
│   │   ├── byte_buffer.c
│   │   ├── byte_buffer.h
│   │   ├── conversions.c
│   │   ├── conversions.h
│   │   ├── libiec61850_platform_includes.h
│   │   ├── linked_list.c
│   │   ├── linked_list.h
│   │   ├── map.c
│   │   ├── map.h
│   │   ├── string_map.c
│   │   ├── string_map.h
│   │   ├── string_utilities.c
│   │   └── string_utilities.h
│   ├── goose
│   │   ├── goose_publisher.c
│   │   ├── goose_publisher.h
│   │   ├── goose_subscriber.c
│   │   ├── goose_subscriber.h
│   │   └── iec61850_goose.asn
│   ├── hal
│   │   ├── byte_stream.c
│   │   ├── byte_stream.h
│   │   ├── ethernet
│   │   │   ├── ethernet.h
│   │   │   ├── linux
│   │   │   │   └── ethernet_linux.c
│   │   │   └── win32
│   │   │       └── ethernet_win32.c
│   │   ├── filesystem
│   │   │   ├── filesystem.h
│   │   │   ├── linux
│   │   │   │   └── file_provider_linux.c
│   │   │   └── win32
│   │   │       └── file_provider_win32.c
│   │   ├── hal.c
│   │   ├── hal.h
│   │   ├── platform_endian.h
│   │   ├── socket
│   │   │   ├── linux
│   │   │   │   └── socket_linux.c
│   │   │   ├── socket.h
│   │   │   └── win32
│   │   │       └── socket_win32.c
│   │   └── thread
│   │       ├── linux
│   │       │   └── thread_linux.c
│   │       ├── thread.h
│   │       └── win32
│   │           └── thread_win32.c
│   ├── iedclient
│   │   ├── iec61850_client.h
│   │   └── impl
│   │       ├── client_control.c
│   │       ├── client_goose_control.c
│   │       ├── client_report.c
│   │       ├── client_report_control.c
│   │       ├── ied_connection.c
│   │       └── ied_connection_private.h
│   ├── iedcommon
│   │   ├── iec61850_common.c
│   │   └── iec61850_common.h
│   ├── iedserver
│   │   ├── iec61850_server.h
│   │   ├── impl
│   │   │   ├── client_connection.c
│   │   │   ├── ied_server.c
│   │   │   └── ied_server_private.h
│   │   ├── mms_mapping
│   │   │   ├── control.c
│   │   │   ├── control.h
│   │   │   ├── mms_goose.c
│   │   │   ├── mms_goose.h
│   │   │   ├── mms_mapping.c
│   │   │   ├── mms_mapping.h
│   │   │   ├── mms_mapping_internal.h
│   │   │   ├── reporting.c
│   │   │   └── reporting.h
│   │   └── model
│   │       ├── cdc.c
│   │       ├── cdc.h
│   │       ├── config_file_parser.c
│   │       ├── config_file_parser.h
│   │       ├── dynamic_model.c
│   │       ├── dynamic_model.h
│   │       ├── model.c
│   │       └── model.h
│   ├── mms
│   │   ├── asn1
│   │   │   ├── asn1_ber_primitive_value.c
│   │   │   ├── asn1_ber_primitive_value.h
│   │   │   ├── ber_decode.c
│   │   │   ├── ber_decode.h
│   │   │   ├── ber_encoder.c
│   │   │   ├── ber_encoder.h
│   │   │   ├── ber_integer.c
│   │   │   └── ber_integer.h
│   │   ├── iso_acse
│   │   │   ├── acse.c
│   │   │   └── acse.h
│   │   ├── iso_client
│   │   │   ├── impl
│   │   │   │   ├── iso_client_connection.c
│   │   │   │   └── iso_connection_parameters.c
│   │   │   ├── iso_client_connection.h
│   │   │   └── iso_connection_parameters.h
│   │   ├── iso_cotp
│   │   │   ├── cotp.c
│   │   │   └── cotp.h
│   │   ├── iso_mms
│   │   │   ├── asn1c
│   │   │   │   ├── AccessResult.c
│   │   │   │   ├── AccessResult.h
│   │   │   │   ├── Address.c
│   │   │   │   ├── Address.h
│   │   │   │   ├── AlternateAccess.c
│   │   │   │   ├── AlternateAccess.h
│   │   │   │   ├── AlternateAccessSelection.c
│   │   │   │   ├── AlternateAccessSelection.h
│   │   │   │   ├── asn_application.h
│   │   │   │   ├── asn_codecs.h
│   │   │   │   ├── asn_codecs_prim.c
│   │   │   │   ├── asn_codecs_prim.h
│   │   │   │   ├── asn_internal.h
│   │   │   │   ├── asn_SEQUENCE_OF.c
│   │   │   │   ├── asn_SEQUENCE_OF.h
│   │   │   │   ├── asn_SET_OF.c
│   │   │   │   ├── asn_SET_OF.h
│   │   │   │   ├── asn_system.h
│   │   │   │   ├── ber_decoder.c
│   │   │   │   ├── ber_decoder.h
│   │   │   │   ├── ber_tlv_length.c
│   │   │   │   ├── ber_tlv_length.h
│   │   │   │   ├── ber_tlv_tag.c
│   │   │   │   ├── ber_tlv_tag.h
│   │   │   │   ├── BIT_STRING.c
│   │   │   │   ├── BIT_STRING.h
│   │   │   │   ├── BOOLEAN.c
│   │   │   │   ├── BOOLEAN.h
│   │   │   │   ├── ConcludeRequestPDU.c
│   │   │   │   ├── ConcludeRequestPDU.h
│   │   │   │   ├── ConcludeResponsePDU.c
│   │   │   │   ├── ConcludeResponsePDU.h
│   │   │   │   ├── ConfirmedErrorPDU.c
│   │   │   │   ├── ConfirmedErrorPDU.h
│   │   │   │   ├── ConfirmedRequestPdu.c
│   │   │   │   ├── ConfirmedRequestPdu.h
│   │   │   │   ├── ConfirmedResponsePdu.c
│   │   │   │   ├── ConfirmedResponsePdu.h
│   │   │   │   ├── ConfirmedServiceRequest.c
│   │   │   │   ├── ConfirmedServiceRequest.h
│   │   │   │   ├── ConfirmedServiceResponse.c
│   │   │   │   ├── ConfirmedServiceResponse.h
│   │   │   │   ├── constraints.c
│   │   │   │   ├── constraints.h
│   │   │   │   ├── constr_CHOICE.c
│   │   │   │   ├── constr_CHOICE.h
│   │   │   │   ├── constr_SEQUENCE.c
│   │   │   │   ├── constr_SEQUENCE.h
│   │   │   │   ├── constr_SEQUENCE_OF.c
│   │   │   │   ├── constr_SEQUENCE_OF.h
│   │   │   │   ├── constr_SET_OF.c
│   │   │   │   ├── constr_SET_OF.h
│   │   │   │   ├── constr_TYPE.c
│   │   │   │   ├── constr_TYPE.h
│   │   │   │   ├── DataAccessError.c
│   │   │   │   ├── DataAccessError.h
│   │   │   │   ├── Data.c
│   │   │   │   ├── Data.h
│   │   │   │   ├── DataSequence.c
│   │   │   │   ├── DataSequence.h
│   │   │   │   ├── DefineNamedVariableListRequest.c
│   │   │   │   ├── DefineNamedVariableListRequest.h
│   │   │   │   ├── DefineNamedVariableListResponse.c
│   │   │   │   ├── DefineNamedVariableListResponse.h
│   │   │   │   ├── DeleteNamedVariableListRequest.c
│   │   │   │   ├── DeleteNamedVariableListRequest.h
│   │   │   │   ├── DeleteNamedVariableListResponse.c
│   │   │   │   ├── DeleteNamedVariableListResponse.h
│   │   │   │   ├── der_encoder.c
│   │   │   │   ├── der_encoder.h
│   │   │   │   ├── FloatingPoint.c
│   │   │   │   ├── FloatingPoint.h
│   │   │   │   ├── GeneralizedTime.c
│   │   │   │   ├── GeneralizedTime.h
│   │   │   │   ├── GetNamedVariableListAttributesRequest.c
│   │   │   │   ├── GetNamedVariableListAttributesRequest.h
│   │   │   │   ├── GetNamedVariableListAttributesResponse.c
│   │   │   │   ├── GetNamedVariableListAttributesResponse.h
│   │   │   │   ├── GetNameListRequest.c
│   │   │   │   ├── GetNameListRequest.h
│   │   │   │   ├── GetNameListResponse.c
│   │   │   │   ├── GetNameListResponse.h
│   │   │   │   ├── GetVariableAccessAttributesRequest.c
│   │   │   │   ├── GetVariableAccessAttributesRequest.h
│   │   │   │   ├── GetVariableAccessAttributesResponse.c
│   │   │   │   ├── GetVariableAccessAttributesResponse.h
│   │   │   │   ├── Identifier.c
│   │   │   │   ├── Identifier.h
│   │   │   │   ├── IndexRangeSeq.c
│   │   │   │   ├── IndexRangeSeq.h
│   │   │   │   ├── InformationReport.c
│   │   │   │   ├── InformationReport.h
│   │   │   │   ├── InitiateErrorPdu.c
│   │   │   │   ├── InitiateErrorPdu.h
│   │   │   │   ├── InitiateRequestPdu.c
│   │   │   │   ├── InitiateRequestPdu.h
│   │   │   │   ├── InitiateResponsePdu.c
│   │   │   │   ├── InitiateResponsePdu.h
│   │   │   │   ├── InitRequestDetail.c
│   │   │   │   ├── InitRequestDetail.h
│   │   │   │   ├── InitResponseDetail.c
│   │   │   │   ├── InitResponseDetail.h
│   │   │   │   ├── Integer16.c
│   │   │   │   ├── Integer16.h
│   │   │   │   ├── Integer32.c
│   │   │   │   ├── Integer32.h
│   │   │   │   ├── Integer8.c
│   │   │   │   ├── Integer8.h
│   │   │   │   ├── INTEGER.c
│   │   │   │   ├── INTEGER.h
│   │   │   │   ├── ListOfVariableSeq.c
│   │   │   │   ├── ListOfVariableSeq.h
│   │   │   │   ├── MmsPdu.c
│   │   │   │   ├── MmsPdu.h
│   │   │   │   ├── MMSString.c
│   │   │   │   ├── MMSString.h
│   │   │   │   ├── NativeEnumerated.c
│   │   │   │   ├── NativeEnumerated.h
│   │   │   │   ├── NativeInteger.c
│   │   │   │   ├── NativeInteger.h
│   │   │   │   ├── NULL.c
│   │   │   │   ├── NULL.h
│   │   │   │   ├── ObjectClass.c
│   │   │   │   ├── ObjectClass.h
│   │   │   │   ├── ObjectName.c
│   │   │   │   ├── ObjectName.h
│   │   │   │   ├── OCTET_STRING.c
│   │   │   │   ├── OCTET_STRING.h
│   │   │   │   ├── ParameterSupportOptions.c
│   │   │   │   ├── ParameterSupportOptions.h
│   │   │   │   ├── per_decoder.c
│   │   │   │   ├── per_decoder.h
│   │   │   │   ├── per_encoder.c
│   │   │   │   ├── per_encoder.h
│   │   │   │   ├── per_support.c
│   │   │   │   ├── per_support.h
│   │   │   │   ├── ReadRequest.c
│   │   │   │   ├── ReadRequest.h
│   │   │   │   ├── ReadResponse.c
│   │   │   │   ├── ReadResponse.h
│   │   │   │   ├── RejectPDU.c
│   │   │   │   ├── RejectPDU.h
│   │   │   │   ├── ScatteredAccessDescription.c
│   │   │   │   ├── ScatteredAccessDescription.h
│   │   │   │   ├── ServiceError.c
│   │   │   │   ├── ServiceError.h
│   │   │   │   ├── ServiceSupportOptions.c
│   │   │   │   ├── ServiceSupportOptions.h
│   │   │   │   ├── StructComponent.c
│   │   │   │   ├── StructComponent.h
│   │   │   │   ├── TimeOfDay.c
│   │   │   │   ├── TimeOfDay.h
│   │   │   │   ├── TypeSpecification.c
│   │   │   │   ├── TypeSpecification.h
│   │   │   │   ├── UnconfirmedPDU.c
│   │   │   │   ├── UnconfirmedPDU.h
│   │   │   │   ├── UnconfirmedService.c
│   │   │   │   ├── UnconfirmedService.h
│   │   │   │   ├── Unsigned16.c
│   │   │   │   ├── Unsigned16.h
│   │   │   │   ├── Unsigned32.c
│   │   │   │   ├── Unsigned32.h
│   │   │   │   ├── Unsigned8.c
│   │   │   │   ├── Unsigned8.h
│   │   │   │   ├── UtcTime.c
│   │   │   │   ├── UtcTime.h
│   │   │   │   ├── UTF8String.c
│   │   │   │   ├── UTF8String.h
│   │   │   │   ├── VariableAccessSpecification.c
│   │   │   │   ├── VariableAccessSpecification.h
│   │   │   │   ├── VariableSpecification.c
│   │   │   │   ├── VariableSpecification.h
│   │   │   │   ├── VisibleString.c
│   │   │   │   ├── VisibleString.h
│   │   │   │   ├── WriteRequest.c
│   │   │   │   ├── WriteRequest.h
│   │   │   │   ├── WriteResponse.c
│   │   │   │   ├── WriteResponse.h
│   │   │   │   ├── xer_decoder.c
│   │   │   │   ├── xer_decoder.h
│   │   │   │   ├── xer_encoder.c
│   │   │   │   ├── xer_encoder.h
│   │   │   │   ├── xer_support.c
│   │   │   │   └── xer_support.h
│   │   │   ├── client
│   │   │   │   ├── mms_client_common.c
│   │   │   │   ├── mms_client_connection.c
│   │   │   │   ├── mms_client_connection.h
│   │   │   │   ├── mms_client_files.c
│   │   │   │   ├── mms_client_get_namelist.c
│   │   │   │   ├── mms_client_get_var_access.c
│   │   │   │   ├── mms_client_identify.c
│   │   │   │   ├── mms_client_initiate.c
│   │   │   │   ├── mms_client_internal.h
│   │   │   │   ├── mms_client_named_variable_list.c
│   │   │   │   ├── mms_client_read.c
│   │   │   │   ├── mms_client_status.c
│   │   │   │   ├── mms_client_write.c
│   │   │   │   └── mms_var_list.c
│   │   │   ├── common
│   │   │   │   ├── mms_common.h
│   │   │   │   ├── mms_common_internal.h
│   │   │   │   ├── mms_common_msg.c
│   │   │   │   ├── mms_device.c
│   │   │   │   ├── mms_device.h
│   │   │   │   ├── mms_device_model.h
│   │   │   │   ├── mms_types.h
│   │   │   │   ├── mms_type_spec.c
│   │   │   │   ├── mms_type_spec.h
│   │   │   │   ├── mms_value.c
│   │   │   │   └── mms_value.h
│   │   │   └── server
│   │   │       ├── mms_access_result.c
│   │   │       ├── mms_access_result.h
│   │   │       ├── mms_association_service.c
│   │   │       ├── mms_domain.c
│   │   │       ├── mms_domain.h
│   │   │       ├── mms_file_service.c
│   │   │       ├── mms_get_namelist_service.c
│   │   │       ├── mms_get_var_access_service.c
│   │   │       ├── mms_identify_service.c
│   │   │       ├── mms_information_report.c
│   │   │       ├── mms_named_variable_list.c
│   │   │       ├── mms_named_variable_list.h
│   │   │       ├── mms_named_variable_list_service.c
│   │   │       ├── mms_read_service.c
│   │   │       ├── mms_server.c
│   │   │       ├── mms_server_common.c
│   │   │       ├── mms_server_connection.c
│   │   │       ├── mms_server_connection.h
│   │   │       ├── mms_server.h
│   │   │       ├── mms_server_internal.h
│   │   │       ├── mms_status_service.c
│   │   │       ├── mms_value_cache.c
│   │   │       ├── mms_value_cache.h
│   │   │       └── mms_write_service.c
│   │   ├── iso_presentation
│   │   │   ├── iso_presentation.c
│   │   │   └── iso_presentation.h
│   │   ├── iso_server
│   │   │   ├── iso_connection.c
│   │   │   ├── iso_server.c
│   │   │   ├── iso_server.h
│   │   │   └── iso_server_private.h
│   │   └── iso_session
│   │       ├── iso_session.c
│   │       └── iso_session.h
│   ├── sampled_values
│   │   ├── sv.asn1
│   │   └── sv_publisher.c
│   └── vs
│       └── stdbool.h

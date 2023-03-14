Here is a simple flow chart:

```mermaid
erDiagram
    referral_groups {
        uuid id PK
        uuid referral_id FK
        uuid group_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    referrals_diagnoses {
        uuid referral_id PK
        uuid diagnosis_id PK
    }

    events {
        text key 
        bigint t 
        character_varying type 
        jsonb data 
    }

    profiles {
        uuid id PK
        character_varying display_name 
        character_varying type 
        character_varying phone 
        uuid schedule_id 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying profile_img_url 
        integer slot_start_buffer_in_s 
        boolean is_global 
        boolean is_active 
        text professional_statement 
        text board_certifications 
        text education_training 
        integer npi_number 
        uuid location_id FK
        character_varying email 
        uuid prescreening_questionnaire_id FK
        character_varying only_allows_gender 
        timestamp_without_time_zone next_availability 
        character_varying prefix 
        character_varying first_name 
        character_varying last_name 
        character_varying suffix 
        boolean is_send_to_provider 
        boolean is_integrated 
        text key 
        integer only_allows_age_min 
        integer only_allows_age_max 
        boolean is_send_to_patient 
        character_varying specialty 
        boolean is_access_center 
        boolean has_consumer_scheduling 
        jsonb tags 
        text general_patient_instructions 
        text referral_search_notice 
        boolean buffer_weekends 
        boolean send_offers 
        boolean is_wait_list 
        jsonb params 
        character_varying slug 
        character_varying group_key 
        boolean are_children_visible 
        boolean has_referral_scheduling 
        integer slot_limit_in_days 
    }

    specialties {
        uuid id PK
        character_varying name 
        boolean is_order_required 
        boolean is_diagnosis_required 
    }

    diagnoses {
        uuid id PK
        character_varying code 
        character_varying description 
    }

    organizations {
        uuid id PK
        character_varying name 
        uuid integration_id 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid region_id FK
        integer max_inactive_user_days 
        character_varying profile_img_url 
        text custom_email_text 
        character_varying slug 
        boolean is_active 
        character_varying custom_email_subject 
        uuid payments_customer_id FK
        uuid access_center_profile_id FK
        boolean is_free 
        boolean show_insurance_filters 
        boolean search_profiles_without_scheduling 
        boolean send_patient_notifications 
        character_varying patient_email_from_address 
        jsonb patient_coverage_map 
        boolean is_covid 
        jsonb tags 
        boolean show_send_to_patient 
        boolean enable_patient_cancellation 
        boolean enable_patient_rescheduling 
        jsonb referral_settings 
        jsonb accelerator_settings 
        uuid free_plan_configuration_id FK
    }

    profiles_procedures {
        uuid profile_id FK
        uuid procedure_id FK
        uuid id PK
        integer duration_in_minutes 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid schedule_id 
    }

    referrals {
        uuid id PK
        text description 
        character_varying status 
        uuid patient_id 
        uuid procedure_id FK
        uuid provider_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid payor_plan_id FK
        character_varying insurance_group_number 
        character_varying insurance_policy_number 
        uuid created_by_user_id FK
        boolean patient_is_pre_authorized 
        uuid matched_payor_id FK
        text result 
        jsonb tags 
        uuid cancelled_by_user_id FK
        timestamp_without_time_zone cancelled_at 
        character_varying cancel_reason 
        boolean is_schedulable 
    }

    workflow_queue_watchers {
        uuid id PK
        uuid workflow_queue_id FK
        uuid user_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    payors {
        uuid id PK
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    payor_plans {
        uuid id PK
        character_varying name 
        uuid payor_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    organization_plans {
        uuid payor_plan_id FK
        uuid organization_id FK
    }

    questionnaire_items {
        uuid id PK
        uuid questionnaire_id FK
        text text 
        character_varying type 
        boolean required 
        character_varying initial_value 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        jsonb options 
        jsonb answer_validators 
        boolean is_active 
        integer order 
        character_varying help_text 
        integer span 
        character_varying reporting_key 
        character_varying mapped_key 
        jsonb depends_on 
        jsonb invalid_answers 
        boolean show_label 
        character_varying key 
        ARRAY upload_accept_types 
        boolean show_other_value_input 
    }

    appointment_syncs {
        uuid organization_id PK
        timestamp_without_time_zone next_sync_at 
        timestamp_without_time_zone last_appointment_updated_at 
    }

    password_resets {
        uuid id PK
        uuid user_id PK
        uuid requested_by_user_id 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    procedures {
        uuid id PK
        character_varying name 
        uuid specialty_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying system 
        character_varying version 
        character_varying code 
        character_varying display 
        character_varying text 
        character_varying cpt_short 
        character_varying cpt_medium 
        text cpt_long 
        text cpt_consumer 
        boolean is_active 
        boolean is_unspecified 
    }

    providers {
        uuid id PK
        character_varying name 
        integer npi 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid location_id FK
        boolean is_active 
        text key 
    }

    appointments {
        uuid id PK
        character_varying status 
        text description 
        timestamp_without_time_zone start 
        timestamp_without_time_zone end 
        text comment 
        uuid fhir_id 
        character_varying time_zone 
        uuid profile_id FK
        uuid referral_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid created_by_user_id FK
        uuid patient_id FK
        uuid procedure_id FK
        jsonb tags 
        jsonb notes 
        uuid rescheduled_to_id FK
        boolean receive_offers 
        text patient_visible_notes 
        uuid directory_id FK
    }

    group_profiles {
        uuid id PK
        uuid group_id FK
        uuid profile_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    appointment_attachments {
        uuid id PK
        character_varying attachment_filename 
        character_varying display_filename 
        uuid appointment_id FK
        timestamp_without_time_zone deleted_at 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying key 
    }

    languages {
        character_varying code PK
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    feature_flags {
        uuid id PK
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    users {
        uuid id PK
        character_varying name 
        character_varying email 
        character_varying password_hash 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        boolean blockit_admin 
        boolean is_active 
        integer login_count 
        integer failed_attempts 
        character_varying current_login_ip 
        character_varying last_login_ip 
        timestamp_without_time_zone locked_at 
        timestamp_without_time_zone deactivated_at 
        timestamp_without_time_zone password_changed_at 
        timestamp_without_time_zone current_login_at 
        timestamp_without_time_zone last_login_at 
        timestamp_without_time_zone last_logout_at 
        character_varying phone 
    }

    samls {
        uuid id PK
        character_varying identity_provider_key 
        character_varying identity_provider_id 
        uuid user_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying idp_id 
    }

    referral_orders {
        uuid id PK
        character_varying order_filename 
        uuid referral_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying display_filename 
        timestamp_without_time_zone deleted_at 
        character_varying type 
    }

    task_appointments {
        uuid id PK
        uuid appointment_id FK
        uuid task_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    task_referrals {
        uuid id PK
        uuid referral_id FK
        uuid task_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    regions {
        uuid id PK
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    tokens {
        uuid id PK
        character_varying username 
        character_varying token 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid organization_id FK
        text notification_emails 
    }

    notification_templates {
        uuid id PK
        uuid organization_id FK
        character_varying name 
        character_varying description 
        character_varying type 
        integer offset 
        character_varying offset_from 
        boolean is_active 
        boolean is_email_active 
        boolean is_sms_active 
        text email_to 
        text email_subject 
        text email_body 
        text sms_to 
        text sms_body 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    cursors {
        character_varying key PK
        bigint t 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    slot_reservations {
        uuid id PK
        uuid slot_id 
        uuid resource_id 
        character_varying token 
        character_varying ip 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    tasks {
        uuid id PK
        character_varying status 
        integer lock_version 
        timestamp_without_time_zone started_at 
        timestamp_without_time_zone finished_at 
        uuid user_id FK
        uuid workflow_queue_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        timestamp_without_time_zone expired_at 
        boolean is_urgent 
    }

    fhir_tokens {
        character_varying name PK
        character_varying token 
        ARRAY organization_ids 
        ARRAY roles 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    user_mappers {
        uuid id PK
        character_varying provider_key 
        character_varying key 
        uuid organization_id FK
        uuid location_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    task_history {
        uuid id PK
        character_varying event 
        uuid user_id FK
        uuid by_user_id FK
        uuid queue_id FK
        uuid task_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    directory_templates {
        uuid id PK
        character_varying name 
        text body 
        uuid directory_id FK
        character_varying hash 
        uuid theme_id 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    itineraries {
        uuid id PK
        date date 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying email 
    }

    webhooks {
        uuid id PK
        character_varying url 
        character_varying method 
        jsonb headers 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    profile_limits {
        uuid id PK
        uuid profile_id 
        character_varying type 
        boolean enabled 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    profile_plans {
        uuid payor_plan_id PK
        uuid profile_id PK
    }

    account_contact_types {
        uuid id PK
        character_varying name 
        character_varying display_name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    directories {
        uuid id PK
        character_varying name 
        citext cname 
        citext domain 
        character_varying password 
        boolean is_active 
        boolean is_password_protected 
        boolean is_maintenance_mode 
        boolean is_domain_verified 
        jsonb settings 
        jsonb filter_settings 
        jsonb sort_settings 
        jsonb patient_form_settings 
        character_varying google_tracking_id 
        uuid organization_id FK
        uuid group_id FK
        timestamp_without_time_zone domain_checked_at 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    appointment_offers {
        uuid id PK
        character_varying phone 
        character_varying status 
        uuid offered_appointment_id FK
        uuid current_appointment_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        timestamp_without_time_zone expires_at 
    }

    group_payor_plans {
        uuid id PK
        uuid group_id FK
        uuid payor_plan_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    free_plan_configurations {
        uuid id PK
        integer profiles 
        integer providers 
        integer locations 
        integer appointments_per_week 
        integer users 
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    procedure_groups {
        uuid id PK
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    directory_sessions {
        uuid id PK
        uuid directory_id FK
        character_varying token 
        timestamp_without_time_zone expires_at 
        jsonb patient_input 
        jsonb search_input 
        jsonb questionnaire_input 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    notification_states {
        uuid id PK
        character_varying state 
        character_varying type 
        uuid appointment_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    audit_logs {
        uuid id PK
        character_varying action 
        uuid record_id 
        uuid user_id 
        jsonb record_context 
        jsonb user_context 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    payor_plan_groups {
        uuid id PK
        character_varying name 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    free_plan_configuration_feature_flags {
        uuid id PK
        uuid free_plan_configuration_id FK
        uuid feature_flag_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    group_procedures {
        uuid id PK
        uuid group_id FK
        uuid procedure_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    invites {
        uuid id PK
        character_varying email 
        character_varying name 
        character_varying organization_name 
        boolean finished 
        boolean bill_recipient 
        boolean approved_for_billing 
        uuid parent_organization_id FK
        uuid child_organization_id FK
        uuid child_user_id FK
        uuid payor_plan_group_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid free_plan_configuration_id FK
        uuid procedure_group_id FK
    }

    profile_languages {
        uuid profile_id FK
        character_varying language_code FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    patient_referrals {
        uuid id PK
        character_varying code 
        timestamp_without_time_zone expires_at 
        uuid profile_id FK
        uuid referral_id FK
        uuid inserted_by_user_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying patient_email 
    }

    locations {
        uuid id PK
        character_varying name 
        character_varying address_1 
        character_varying address_2 
        character_varying city 
        character_varying state 
        character_varying postal_code 
        character_varying country 
        double_precision latitude 
        double_precision longitude 
        character_varying time_zone 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying phone 
        text key 
        character_varying slug 
        boolean is_active 
        jsonb params 
    }

    user_locations {
        uuid id PK
        uuid location_id FK
        uuid user_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    user_organizations {
        uuid id PK
        uuid organization_id FK
        uuid user_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        boolean is_default 
        boolean email_notifications 
        boolean is_admin 
        boolean has_all_locations 
        boolean is_editor 
        boolean sms_notifications 
    }

    organization_feature_flags {
        uuid id PK
        uuid organization_id FK
        uuid feature_flag_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    groups {
        uuid id PK
        character_varying name 
        boolean is_referral_network 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        boolean is_active 
        integer order_by 
        boolean is_all_locations 
        boolean is_itinerary 
        boolean is_region_restricted 
    }

    questionnaires {
        uuid id PK
        character_varying name 
        character_varying title 
        character_varying status 
        character_varying subject_type 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        uuid procedure_id FK
        integer order 
        jsonb apply_filters 
        character_varying type 
        uuid workflow_queue_id FK
        character_varying placement 
        boolean show_title 
        jsonb filter_mappers 
        boolean is_active 
    }

    group_locations {
        uuid id PK
        uuid group_id FK
        uuid location_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    group_organizations {
        uuid id PK
        uuid group_id FK
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    usages {
        uuid id PK
        date date 
        integer count 
        uuid organization_id FK
        character_varying service 
    }

    pelitas {
        uuid id PK
        date date 
        integer calls 
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    organization_consumer_scheduling_settings {
        uuid id PK
        uuid organization_id FK
        boolean allow_attachments 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        boolean search_insurance 
        character_varying visit_type_form_label 
        text html_header 
        text html_footer 
        text html_head_tags 
        character_varying google_tag_manager_id 
        boolean search_providers 
        boolean show_languages 
        boolean show_patient_prefill 
        jsonb form_field_settings 
        boolean show_map 
        character_varying no_availability_text 
        character_varying no_availability_action 
    }

    workflow_queues {
        uuid id PK
        character_varying name 
        character_varying trigger_type 
        character_varying trigger_status_from 
        character_varying trigger_status_to 
        uuid organization_id FK
        boolean is_active 
        jsonb apply_filters 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        integer expiration_in_s 
        boolean manual_trigger 
        character_varying color 
        boolean show_related_queues 
        boolean show_schedule_button 
        boolean show_accept_button 
        integer order 
        character_varying template 
        boolean is_internal 
        boolean is_dead_letter 
        uuid dead_letter_queue_id FK
        text task_description 
        boolean task_order_by_desc 
        boolean task_order_by_owner 
        boolean supports_urgent_tasks 
        boolean finish_tasks_after_reschedule 
    }

    external_services {
        uuid id PK
        character_varying name 
        character_varying type 
        boolean is_active 
        uuid organization_id FK
        jsonb params 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    hl7_configs {
        uuid id PK
        uuid token_id FK
        uuid organization_id FK
        jsonb routes 
        jsonb patient 
        jsonb coverage 
        jsonb schedule 
        jsonb appointment 
        jsonb location 
        jsonb profile 
        jsonb referral 
        jsonb provider 
        jsonb maps 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        boolean active 
        character_varying type 
    }

    account_contacts {
        uuid id PK
        character_varying name 
        character_varying email 
        character_varying phone 
        boolean receives_marketing 
        text comment 
        uuid account_contact_type_id FK
        uuid organization_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    group_providers {
        uuid id PK
        uuid group_id FK
        uuid provider_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    directory_pages {
        uuid id PK
        uuid directory_id FK
        character_varying type 
        character_varying path 
        boolean is_active 
        character_varying redirect_to 
        character_varying name 
        character_varying title 
        text body 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying template_name 
    }

    directory_keywords {
        uuid id PK
        character_varying term 
        jsonb search_input 
        uuid directory_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying redirect_to 
    }

    directory_locale_strings {
        uuid id PK
        character_varying locale 
        character_varying key 
        character_varying value 
        uuid directory_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    profile_referrals {
        uuid id PK
        uuid profile_id FK
        uuid referral_id FK
        uuid inserted_by_user_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
        character_varying patient_email 
    }

    messages {
        uuid id PK
        uuid user_id FK
        uuid referral_id FK
        text body 
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    itinerary_appointments {
        uuid id PK
        uuid itinerary_id FK
        uuid appointment_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    task_comments {
        uuid id PK
        text body 
        uuid user_id FK
        uuid task_id FK
        timestamp_without_time_zone inserted_at 
        timestamp_without_time_zone updated_at 
    }

    referral_groups }o--|| referrals : "referral_id"
    referral_groups }o--|| groups : "group_id"
    referrals_diagnoses }o--|| referrals : "referral_id"
    referrals_diagnoses }o--|| diagnoses : "diagnosis_id"
    profiles }o--|| organizations : "organization_id"
    profiles_procedures }o--|| profiles : "profile_id"
    appointments }o--|| profiles : "profile_id"
    group_profiles }o--|| profiles : "profile_id"
    profile_languages }o--|| profiles : "profile_id"
    profiles }o--|| locations : "location_id"
    profiles }o--|| questionnaires : "prescreening_questionnaire_id"
    profile_plans }o--|| profiles : "profile_id"
    patient_referrals }o--|| profiles : "profile_id"
    profile_referrals }o--|| profiles : "profile_id"
    organizations }o--|| profiles : "access_center_profile_id"
    procedures }o--|| specialties : "specialty_id"
    providers }o--|| organizations : "organization_id"
    user_organizations }o--|| organizations : "organization_id"
    organization_feature_flags }o--|| organizations : "organization_id"
    groups }o--|| organizations : "organization_id"
    organization_plans }o--|| organizations : "organization_id"
    organizations }o--|| free_plan_configurations : "free_plan_configuration_id"
    locations }o--|| organizations : "organization_id"
    questionnaires }o--|| organizations : "organization_id"
    group_organizations }o--|| organizations : "organization_id"
    organizations }o--|| regions : "region_id"
    organization_consumer_scheduling_settings }o--|| organizations : "organization_id"
    user_mappers }o--|| organizations : "organization_id"
    usages }o--|| organizations : "organization_id"
    pelitas }o--|| organizations : "organization_id"
    workflow_queues }o--|| organizations : "organization_id"
    notification_templates }o--|| organizations : "organization_id"
    external_services }o--|| organizations : "organization_id"
    hl7_configs }o--|| organizations : "organization_id"
    account_contacts }o--|| organizations : "organization_id"
    webhooks }o--|| organizations : "organization_id"
    directories }o--|| organizations : "organization_id"
    invites }o--|| organizations : "parent_organization_id"
    invites }o--|| organizations : "child_organization_id"
    tokens }o--|| organizations : "organization_id"
    profiles_procedures }o--|| procedures : "procedure_id"
    referrals }o--|| payors : "matched_payor_id"
    referrals }o--|| procedures : "procedure_id"
    referrals }o--|| providers : "provider_id"
    referrals }o--|| payor_plans : "payor_plan_id"
    referral_orders }o--|| referrals : "referral_id"
    referrals }o--|| users : "created_by_user_id"
    messages }o--|| referrals : "referral_id"
    patient_referrals }o--|| referrals : "referral_id"
    profile_referrals }o--|| referrals : "referral_id"
    appointments }o--|| referrals : "referral_id"
    task_referrals }o--|| referrals : "referral_id"
    referrals }o--|| users : "cancelled_by_user_id"
    workflow_queue_watchers }o--|| workflow_queues : "workflow_queue_id"
    workflow_queue_watchers }o--|| users : "user_id"
    payor_plans }o--|| payors : "payor_id"
    organization_plans }o--|| payor_plans : "payor_plan_id"
    group_payor_plans }o--|| payor_plans : "payor_plan_id"
    profile_plans }o--|| payor_plans : "payor_plan_id"
    questionnaire_items }o--|| questionnaires : "questionnaire_id"
    appointments }o--|| procedures : "procedure_id"
    questionnaires }o--|| procedures : "procedure_id"
    group_procedures }o--|| procedures : "procedure_id"
    providers }o--|| locations : "location_id"
    group_providers }o--|| providers : "provider_id"
    notification_states }o--|| appointments : "appointment_id"
    notification_states }o--|| appointments : "appointment_id"
    appointments }o--|| users : "created_by_user_id"
    task_appointments }o--|| appointments : "appointment_id"
    task_appointments }o--|| appointments : "appointment_id"
    appointment_attachments }o--|| appointments : "appointment_id"
    appointment_attachments }o--|| appointments : "appointment_id"
    itinerary_appointments }o--|| appointments : "appointment_id"
    itinerary_appointments }o--|| appointments : "appointment_id"
    appointments }o--|| appointments : "rescheduled_to_id"
    appointments }o--|| appointments : "rescheduled_to_id"
    appointment_offers }o--|| appointments : "offered_appointment_id"
    appointment_offers }o--|| appointments : "offered_appointment_id"
    appointment_offers }o--|| appointments : "current_appointment_id"
    appointment_offers }o--|| appointments : "current_appointment_id"
    appointments }o--|| directories : "directory_id"
    group_profiles }o--|| groups : "group_id"
    profile_languages }o--|| languages : "language_code"
    organization_feature_flags }o--|| feature_flags : "feature_flag_id"
    free_plan_configuration_feature_flags }o--|| feature_flags : "feature_flag_id"
    user_organizations }o--|| users : "user_id"
    user_locations }o--|| users : "user_id"
    samls }o--|| users : "user_id"
    messages }o--|| users : "user_id"
    patient_referrals }o--|| users : "inserted_by_user_id"
    profile_referrals }o--|| users : "inserted_by_user_id"
    tasks }o--|| users : "user_id"
    task_history }o--|| users : "user_id"
    task_history }o--|| users : "by_user_id"
    task_comments }o--|| users : "user_id"
    invites }o--|| users : "child_user_id"
    task_appointments }o--|| tasks : "task_id"
    task_referrals }o--|| tasks : "task_id"
    hl7_configs }o--|| tokens : "token_id"
    tasks }o--|| workflow_queues : "workflow_queue_id"
    task_history }o--|| tasks : "task_id"
    task_comments }o--|| tasks : "task_id"
    user_mappers }o--|| locations : "location_id"
    task_history }o--|| workflow_queues : "queue_id"
    directory_templates }o--|| directories : "directory_id"
    itinerary_appointments }o--|| itineraries : "itinerary_id"
    account_contacts }o--|| account_contact_types : "account_contact_type_id"
    directories }o--|| groups : "group_id"
    directory_pages }o--|| directories : "directory_id"
    directory_keywords }o--|| directories : "directory_id"
    directory_locale_strings }o--|| directories : "directory_id"
    directory_sessions }o--|| directories : "directory_id"
    group_payor_plans }o--|| payor_plan_groups : "group_id"
    free_plan_configuration_feature_flags }o--|| free_plan_configurations : "free_plan_configuration_id"
    invites }o--|| free_plan_configurations : "free_plan_configuration_id"
    invites }o--|| procedure_groups : "procedure_group_id"
    group_procedures }o--|| procedure_groups : "group_id"
    invites }o--|| payor_plan_groups : "payor_plan_group_id"
    group_locations }o--|| locations : "location_id"
    user_locations }o--|| locations : "location_id"
    group_locations }o--|| groups : "group_id"
    group_providers }o--|| groups : "group_id"
    group_organizations }o--|| groups : "group_id"
    questionnaires }o--|| workflow_queues : "workflow_queue_id"
    workflow_queues }o--|| workflow_queues : "dead_letter_queue_id"
```

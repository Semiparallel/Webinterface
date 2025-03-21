<script lang="ts">
    import { page } from "$app/stores";
    import ChannelSelector from "$lib/components/settings/channelSelector.svelte";
    import MassDataSetup from "$lib/components/settings/massDataSetup.svelte";
    import MessageSelector from "$lib/components/settings/messageSelector.svelte";
    import { currentServer } from "$lib/scripts/servers";

</script>

<svelte:head>
    <title>Interactions - { $currentServer.name }</title>
</svelte:head>

<h1 class="headline">Tickets</h1>

<MassDataSetup icon="confirmation_number" title="Ticket system" description="Setup the ticket system." endpoint={"/guilds/" + $page.params.serverId + "/tickets"}
model={[
    {
        name: "Ticket creation channel",
        jsonName: "channelId",
        type: "channel",
        unit: "",
        value: {
            id: null,
            name: null,
            type: "TEXT"
        },
        visible: true,
        jsonResName: "channel"
    },
    {
        name: "Logging channel",
        jsonName: "logChannelId",
        type: "channel",
        unit: "CATEGORY",
        value: {
            id: null,
            name: null,
            type: "TEXT"
        },
        visible: true,
        jsonResName: "logChannel"
    }
]}

isEnabled={(json) => {
    return json.channel != null
}}

primaryIcon="check"
render={(json) => {
    return json.ticketCount + " tickets with logging in #" + json.logChannel.name + " and ticket creation in #" + json.channel.name + "."
}}

/>

<div class="default-margin"></div>

<MessageSelector icon="menu_open" title="Ticket opening message" description="Configure the message sent when opening a ticket." settingName="message_ticket_open"/>

<div class="default-margin"></div>

<MessageSelector icon="sticky_note_2" title="Ticket menu message" description="Configure the message in the ticket creation embed." settingName="message_ticket_menu"/>

<h1 class="headline">Suggestions</h1>

<ChannelSelector icon="tag" title="Suggestions channel" description="Select the channel for all suggestions." endpoint={"/guilds/" + $page.params.serverId + "/suggestions"} />

<div class="default-margin"></div>

<MessageSelector icon="sticky_note_2" title="Suggestions embed message" description="Configure the message that will be shown in the suggestions embed." settingName="message_suggestion_menu"/>

<h1 class="headline">Temporal voice channel</h1>

<ChannelSelector icon="mic" title="Temporal voice channel" type="VOICE" description="Select the channel that creates new temporal voice channels." endpoint={"/guilds/" + $page.params.serverId + "/temporalvoice"} />

<style lang="scss">
    @import '$lib/default.scss';
    @import '$lib/styles/box.scss';
    @import '$lib/styles/chips.scss';

    .chip-button {
        margin-left: 0.1rem;
        color: var(--seasalt);
        transition: 250ms ease;

        &:hover {
            color: var(--primary);
        }
    }

</style>
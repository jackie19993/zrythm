# Import necessary libraries for MIDI file creation
# You might need to install 'mido' if you haven't already:
# pip install mido
import mido

# Define common MIDI notes for a basic scale (C Major starting at C4)
NOTES = {
    'C': 60, 'C#': 61, 'Db': 61, 'D': 62, 'D#': 63, 'Eb': 63,
    'E': 64, 'F': 65, 'F#': 66, 'Gb': 66, 'G': 67, 'G#': 68,
    'Ab': 68, 'A': 69, 'A#': 70, 'Bb': 70, 'B': 71
}

# Define common chord intervals (in semitones)
CHORD_INTERVALS = {
    'major': [0, 4, 7],
    'minor': [0, 3, 7],
    'dominant7': [0, 4, 7, 10],
    'major7': [0, 4, 7, 11],
    'minor7': [0, 3, 7, 10]
}

def create_midi_chords(filename, bpm=120, chords_sequence=None, note_length=1.0):
    """
    Generates a MIDI file with a sequence of chords.
    """
    if chords_sequence is None:
        chords_sequence = [] # Ensure it's not None if no sequence is passed

    mid = mido.MidiFile()
    track = mido.MidiTrack()
    mid.tracks.append(track)

    tempo = mido.bpm2tempo(bpm)
    track.append(mido.Message('set_tempo', tempo=tempo, time=0))

    ticks_per_beat = mid.ticks_per_beat
    ticks_per_note = int(ticks_per_beat * note_length)

    for i, (root_note_str, chord_type, octave) in enumerate(chords_sequence):
        if root_note_str not in NOTES or chord_type not in CHORD_INTERVALS:
            print(f"Warning: Invalid chord data ({root_note_str}, {chord_type}). Skipping.")
            continue

        base_midi_note = NOTES[root_note_str] + (octave - 4) * 12
        intervals = CHORD_INTERVALS[chord_type]

        for j, interval in enumerate(intervals):
            note = base_midi_note + interval
            velocity = 64
            track.append(mido.Message('note_on', note=note, velocity=velocity, time=0))

        for j, interval in enumerate(intervals):
            note = base_midi_note + interval
            velocity = 0
            time_for_note_off = ticks_per_note if j == len(intervals) - 1 else 0
            track.append(mido.Message('note_off', note=note, velocity=velocity, time=time_for_note_off))

    mid.save(filename)
    print(f"MIDI file '{filename}' created successfully!")

# --- Generate the "Mele Pelo Le Moya" hymn-like MIDI files ---
if __name__ == '__main__':
    print("Creating 'mele_pelo_le_moya_hymn.mid' (C Major based)...")
    hymn_chords_C = [
        ('C', 'major', 4), # I
        ('F', 'major', 4), # IV
        ('G', 'major', 4), # V
        ('C', 'major', 4), # I
        ('C', 'major', 4), # Repeat C for longer sections
        ('F', 'major', 4),
        ('C', 'major', 4),
        ('G', 'major', 4),
        ('C', 'major', 4)
    ]
    create_midi_chords('mele_pelo_le_moya_hymn.mid', bpm=90, chords_sequence=hymn_chords_C, note_length=1.5)

    print("Creating 'mele_pelo_le_moya_hymn_G.mid' (G Major based)...")
    hymn_chords_G = [
        ('G', 'major', 4), # I
        ('C', 'major', 4), # IV
        ('D', 'major', 4), # V
        ('G', 'major', 4), # I
        ('G', 'major', 4),
        ('C', 'major', 4),
        ('G', 'major', 4),
        ('D', 'major', 4),
        ('G', 'major', 4)
    ]
    create_midi_chords('mele_pelo_le_moya_hymn_G.mid', bpm=90, chords_sequence=hymn_chords_G, note_length=1.5)
